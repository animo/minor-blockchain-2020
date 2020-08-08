# Week 3: Security And Saving Gas

## Smart Contracts

It is important to stress how purely functional a smart contract is. The code, once deployed, cannot be changed. Additionally the smart contract only acts when called by a transaction from a user and will always execute in the same way when the same actions and/or data are presented (it is **deterministic**). It is not flexible and it is not independent. To change a smart contract a new smart contract needs to be created. This means that the code needs to be foolproof before it is deployed to the blockchain.

TODO DAO Hack

## Ethereum

The previous week we learned that executing smart contracts is not free. Every operation involved in the process has some amount of computational effort involves (measured in Gas). To make this effort miners need to be payed in Ether. Because every operation costs money, it is important to be aware of cost efficient strategies when making smart contracts.

<!-- 2. Gas & gas cost & saving gas (view functions, structs, storage) -->

"As mentioned previously, it is important to remember that a contract’s code cannot be changed. However, a contract can be “deleted,” removing the code and its internal state (storage) from its address, leaving a blank account. Any transactions sent to that account address after the contract has been deleted do not result in any code execution, because there is no longer any code there to execute. To delete a contract, you execute an EVM opcode called SELFDESTRUCT (previously called SUICIDE). That operation costs “negative gas,” a gas refund, thereby incentivizing the release of network client resources from the deletion of stored state. Deleting a contract in this way does not remove the transaction history (past) of the contract, since the blockchain itself is immutable. It is also important to note that the SELFDESTRUCT capability will only be available if the contract author programmed the smart contract to have that functionality. If the contract’s code does not have a SELFDESTRUCT opcode, or it is inaccessible, the smart contract cannot be deleted."
https://github.com/ethereumbook/ethereumbook/blob/develop/07smart-contracts-solidity.asciidoc#what-is-a-smart-contract

## Solidity

A lot of the concepts from the last lessons are relevant to security. Visibility types determine who gets to call a function, addresses and the require function allow conditional code execution etc.

When writing smart contract code in Solidity it is important to be aware of the consequences of using these different types and functions. Examine public and external functions and think about if they can be used in a way that contradicts how you want the smart contract to function.

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

### Functions

#### Modifiers

Function modifiers are used to modify the behavior of functions. They create additional features or make sure there are restrictions on a function. In week 1 the **view** and **pure** modifiers where discussed. It is also possible to define a new modifier.

In the previouw 'owning a contract' section, the 'onlyOwner' modifier was used. This modifier is created to enforce the restriction that the person who calls the function needs to be the owner of the contract.

```solidity
modifier onlyOwner () {
  require(msg.sender == owner);
  _;
}
```

The underscore is the placeholder for the function that uses the modifier. The placement of the underscore determines if the modifier is executed before or after the original function.

Modifiers can be simple (like onlyOwner) or complex depending on what you need them to do. They can also take arguments.

```solidity
    // creating the mapping
    mapping(address => uint) public userLevel;

    modifier higherThan(uint level, address userAddress){
        require(userLevel[userAddress] > level)
    }
```

<!-- variables, types, functions (visibility), events --

#### For loops

#### Time




3. Using other contracts
4. Backdoors
5. Functions 3: functions revenge

   - structs as arguments

6. Time
7. For loops
