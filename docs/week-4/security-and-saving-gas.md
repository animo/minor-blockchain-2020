# Week 4: Security And Saving Gas

## Smart Contracts

It is important to stress how purely functional a smart contract is. The code, once deployed, cannot be changed. Additionally the smart contract only acts when called by a transaction from a user and will always execute in the same way when the same actions and/or data are presented (it is **deterministic**). It is not flexible and it is not independent. To change a smart contract a new smart contract needs to be created. This means that if there is a security weakness it is very difficult to fix, especially because everyone can see the code and can therefore take advantage of the weakness before it is fixed. This means that the code needs to be foolproof before it is deployed to the blockchain.

//TODO extend

## Ethereum

### Security

There are several big security stories in the history of the Ethereum network, but the most famous is The DAO Hack that happened in June 2016.

A decentralized autonomous organization (DAO) is an organization that functions in a decentralized way. The organization itself is run by smart contract code. Initially the DAO is funded by people who buy shares in the organization in the form of **tokens** (more on tokens later). During this funding round a lot of money can be put into the DAO. The DAO itself is not _owned_ by anyone, but people who own shares have voting power.

A decentralized autonomous organization called 'The DAO' had a very big crowdfunding round. They raised 150 million dollar to fund this project in a period of 28 days. The project was a smart contract that allowed funding of proposals. Once the funding period was over, people who owned shares would be able to vote on proposals. The proposals that win the voting are then funded by the money that was raised.

Vulnerabilities in the smart contracts code were discovered early on, but fixing these vulnerabilities was delayed until after funding. While a team was working on fixing the bug, a hacker took advantage and was able to transfer over 50 million dollar to another smart contract.

The interesting thing about this is that code on the Ethereum network is transparent, as are transactions. So the amount of money in The DAO contract and in the hackers smart contract was visible. The world was waiting to see what would happen to the money in both The DAO and the hackers smart contract. It was stuck in a way. Kind of like a bank robber hiding the money and then having to find a way to return. Meanwhile the Ethereum Foundation was working on a way to fix this.

Two fixes were proposed. The 'soft fork' fix proposed to make a change in the network that any code that tries to access The DAO contract or the hackers contract is invalid and does not work. The Ethereum Foundation could not just implement this fix because blockchain is decentralized. To implement this, the network needed 51% of nodes to agree to this new truth, whereas the whole foundation of blockchain is that this does **not** happen. The 'hard fork' fix proposed a refund system where people who lost money could request it back from The DAO contract. A vote was held and the hard fork solution won.

As a result of this plan the Ethereum network was split, the original blockchain was named Ethereum Classic and Ethereum continued.

The weakness that allowed the DAO hack to happen was **not** an Ethereum weakness. It was a weakness in the smart contract code written for The DAO application. This is one way in which the immutability of blockchain and smart contract code can work against usability.

### Saving Gas

The previous week we learned that executing smart contracts is not free. Every operation involved in the process has some amount of computational effort involves (measured in Gas). To make this effort miners need to be payed in Ether. Because every operation costs money, it is important to be aware of cost efficient strategies when making smart contracts.

<!-- what costs a lot, what doesn't -->

There are multiple strategies to save on operation costs, using uint subtypes inside of structs, ...., .....

<!-- 2. Gas & gas cost & saving gas (view functions, structs, storage) -->

"As mentioned previously, it is important to remember that a contract’s code cannot be changed. However, a contract can be “deleted,” removing the code and its internal state (storage) from its address, leaving a blank account. Any transactions sent to that account address after the contract has been deleted do not result in any code execution, because there is no longer any code there to execute. To delete a contract, you execute an EVM opcode called SELFDESTRUCT (previously called SUICIDE). That operation costs “negative gas,” a gas refund, thereby incentivizing the release of network client resources from the deletion of stored state. Deleting a contract in this way does not remove the transaction history (past) of the contract, since the blockchain itself is immutable. It is also important to note that the SELFDESTRUCT capability will only be available if the contract author programmed the smart contract to have that functionality. If the contract’s code does not have a SELFDESTRUCT opcode, or it is inaccessible, the smart contract cannot be deleted."
https://github.com/ethereumbook/ethereumbook/blob/develop/07smart-contracts-solidity.asciidoc#what-is-a-smart-contract

## Solidity

A lot of the concepts from the last lessons are relevant to security. Visibility types determine who gets to call a function, addresses and the require function allow conditional code execution etc.

When writing smart contract code in Solidity it is important to be aware of the consequences of using these different types and functions. Look at all public and external functions and ask yourself if they can be used in a way that contradicts how you want the smart contract to function.

### Owning a contract

One security measure that is often implemented is to have a contract owner. Once a smart contract has an owner (is ownable) it can implement functions that work only for the owner. Previously the concept of inheritance was discussed. The Ownable contract is a great example of the use of inheritance.

The easiest way to be able to limit functions to an owner is to make your smart contract inherit from a previously designed Ownable contract.

```solidity
contract MemberList is Ownable {
   mapping (address => bool) members;

   // Calling the constructor makes the address that deploys this contract the owner of the contract
   constructor() public Ownable() {
   }

   // The 'onlyOwner' modifier makes the function turn back if it is not called by the owner of the contract.
   function addMember(address _member)
       public
       onlyOwner
   {
       members[_member] = true;
   }
}
```

It has come up a lot that the code of a smart contract cannot change (remember immutability). It _is_ possible however for smart contract to contain functions that, when called, change certain information within the contract.

An example for this is the owner of a contract. If you want to change the owner, you do not want to make and deploy a new smart contract. Instead you can create a function that can change who the owner is.

```solidity
    // very simple transfer function
    // note that only the current owner can call this function with the 'onlyOwner' modifier
    function transferOwnership(address newOwner) public onlyOwner {
        owner = newOwner;
    }
```

### Functions

#### Custom Modifiers

Function modifiers are used to modify the behavior of functions. They create additional features or make sure there are restrictions on a function. Visibility modifiers and state modifiers have been discussed already. It is also possible to define a custom modifier with custom logic.

In the previous 'owning a contract' section, the 'onlyOwner' modifier was used. This modifier is created to enforce the restriction that the person who calls the function needs to be the owner of the contract.

```solidity
modifier onlyOwner () {
  require(msg.sender == owner);
  _;
}
```

The underscore (\_) is the placeholder for the function that uses the modifier. The placement of the underscore determines if the modifier is executed before or after the original function.

Modifiers can be simple (like onlyOwner) or complex depending on what you need them to do. They can also take arguments.

```solidity
    // creating the mapping
    mapping(address => uint) public userLevel;

    modifier higherThan(uint level, address userAddress){
        require(userLevel[userAddress] > level)
    }
```

### Time

TODO: Optional.... lesson 3 chapter 5, 6

TODO: RECURRING CONTRACT

### Storage pointers

<!-- Storage pointers? Memory and storage, calldata -->

In previous lessons memory and storage where mentioned briefly. Any variable saved in storage is saved permanently on the blockchain, while anything saved in memory is saved temporarily and forgotten after the action that needs it is finished.

The way we can mostly tell the difference is that storage variables are defined outside of functions, while memory variables are defined within functions.

Whether a variable should be saved in storage or memory can also be explicitly mentioned. This comes into play when we are trying to save Gas (remember, storage is more expensive than memory).

// TODO expand

### Additional reading / watching

[Understanding The DAO Attack](https://www.coindesk.com/understanding-dao-hack-journalists)
[The Dao: The Hack, The Soft Fork and The Hard Fork](https://www.cryptocompare.com/coins/guides/the-dao-the-hack-the-soft-fork-and-the-hard-fork/)
