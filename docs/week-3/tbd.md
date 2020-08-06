# Week 3: Security

## Smart Contracts :

It is important to stress how purely functional a smart contract is. The code, once deployed, cannot be changed. Additionally the smart contract only acts when called by a transaction from a user and will always execute in the same way when the same actions and/or data are presented (it is **deterministic**). It is not flexible and it is not independent. This means that it needs to be foolproof before it is deployed.

DAO Hack

## Ethereum :

The previous week we learned that executing smart contracts is not free. Every operation involved in the process has some amount of computational effort involves (measured in Gas). To make this effort miners need to be payed in Ether. Because every operation costs money, it is important to be aware of cost efficient strategies when making smart contracts.

"As mentioned previously, it is important to remember that a contract’s code cannot be changed. However, a contract can be “deleted,” removing the code and its internal state (storage) from its address, leaving a blank account. Any transactions sent to that account address after the contract has been deleted do not result in any code execution, because there is no longer any code there to execute. To delete a contract, you execute an EVM opcode called SELFDESTRUCT (previously called SUICIDE). That operation costs “negative gas,” a gas refund, thereby incentivizing the release of network client resources from the deletion of stored state. Deleting a contract in this way does not remove the transaction history (past) of the contract, since the blockchain itself is immutable. It is also important to note that the SELFDESTRUCT capability will only be available if the contract author programmed the smart contract to have that functionality. If the contract’s code does not have a SELFDESTRUCT opcode, or it is inaccessible, the smart contract cannot be deleted."
https://github.com/ethereumbook/ethereumbook/blob/develop/07smart-contracts-solidity.asciidoc#what-is-a-smart-contract

## Solidity :

<!-- variables, types, functions (visibility), events --
