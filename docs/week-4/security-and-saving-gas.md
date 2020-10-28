# Security And Saving Gas

- [Security And Saving Gas](#security-and-saving-gas)
  - [Smart Contracts](#smart-contracts)
  - [Ethereum](#ethereum)
    - [Security](#security)
    - [Saving Gas](#saving-gas)
  - [Deleting Smart Contracts](#deleting-smart-contracts)
  - [Solidity](#solidity)
    - [Owning a contract](#owning-a-contract)
    - [Functions](#functions)
      - [Custom Modifiers](#custom-modifiers)
    - [Time](#time)
    - [Storage pointers](#storage-pointers)
  - [Additional reading / watching](#additional-reading--watching)

## Smart Contracts

It is important to stress how purely functional a smart contract is. The code, once deployed, cannot be changed. Additionally the smart contract only acts when called by a transaction from a user and will always execute in the same way when the same actions and/or data are presented (it is **deterministic**). It is not flexible and it is not independent.

To change a smart contract a new smart contract needs to be created. This means that if there is a security weakness it is very difficult to fix, especially because everyone can see the code (**transparency**) and can therefore take advantage of the weakness before it is fixed. This means that the code needs to be foolproof before it is deployed to the blockchain.

Another thing that makes smart contracts vulnerable is that they are in many cases so undeniably linked to money. It is visible to the world where this money is stored. Not even really the world. It is visible to a group of people who are often very technologically capable, who value anonymity and who enjoy the challenge of finding errors in code. It will be interesting to see in the coming years how security (and legal processes) will evolve for smart contracts.

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

February 2020 the IOTA network was shut down because of a hack that exploited a vulnerability in their app to steal around 1.6 million dollars from users (this amount was suggested by open-source reportings, it is unconfirmed by IOTA). IOTA is not blockchain, it is a distributed ledger technology that uses a non-linear 'tangle' instead of blockchain. Because of this the IOTA Foundation was able to just shut down the entire network. IOTA received a lot of negative press for this action as it goes against some core philosophies of these types of network.

Blockchain offers pro's and con's in terms of its immutability vs. flexibility. These security cases show that there is not necessarily one right answer. But most of all they show that when writing smart contract code you better double and triple check for vulnerabilities before deploying to the network.

### Saving Gas

The previous week we learned that executing smart contracts is not free. Every operation involved in the process has some amount of computational effort involves (measured in Gas). To make this effort miners need to be payed in Ether. Because every operation costs money, it is important to be aware of cost efficient strategies when making smart contracts. They need to be **optimized**.

There are multiple strategies to save on operation costs. These strategies are based on the cost of certain actions on the Ethereum network. Changing something or adding (storing) something costs gas, while simply viewing information often does not. So every storage space and call should be optimized. There are other cost elements, like how mappings are often cheaper than arrays and if your function is external it is better to use the modifier external than public based on cost. There are refunds for freeing up storage space, so the less room on the blockchain your code takes up the better.

## Deleting Smart Contracts

A smart contracts code can not be changed once it is deployed. However, a smart contract can be deleted. Deleting a smart contract removes everything from the address. After it is deleted all transactions that are sent to the address are not executed. Because the blockchain is immutable, the history of the contract is never deleted and will always stay on the blockchain.

The way to delete a smart contract starts with the fact that the code cannot be changed. The developer of the smart contract needs to have built in the possibility do delete it. This is done through a function called selfdestruct. The operation selfdestruct also enables a gas refund (by making the transaction cost negative gas) so any stored money or other resources can be 'freed' from the contract.

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

    modifier higherThan(uint _level, address _userAddress){
        require(userLevel[_userAddress] > _level)
    }

```

### Time

TODO: Optional.... lesson 3 chapter 5, 6 in cryptozombies

TODO: RECURRING CONTRACT

### Storage pointers

In previous lessons memory and storage where mentioned briefly. Any variable saved in storage is saved permanently on the blockchain, while anything saved in memory is saved temporarily and forgotten after the action that needs it is finished.

The way we can mostly tell the difference is that storage variables are defined outside of functions, while memory variables are defined within functions. When these are mentioned explicitly we speak about storage pointers.

Whether a variable should be saved in storage or memory can also be explicitly mentioned. This comes into play when we are trying to save Gas (remember, storage is more expensive than memory).

## Additional reading / watching

[Understanding The DAO Attack](https://www.coindesk.com/understanding-dao-hack-journalists)
[The Dao: The Hack, The Soft Fork and The Hard Fork](https://www.cryptocompare.com/coins/guides/the-dao-the-hack-the-soft-fork-and-the-hard-fork/)
[Storage Pointers in Solidity](https://blog.b9lab.com/storage-pointers-in-solidity-7dcfaa536089)
