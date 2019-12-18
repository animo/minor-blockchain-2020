<!-- omit in toc -->
# Solidity Cheatsheet Lesson 1

- [Basic contract structure](#basic-contract-structure)
  - [Compiler Version](#compiler-version)
  - [Contract Declaration](#contract-declaration)
- [Variables](#variables)
  - [Primitive Value Types](#primitive-value-types)
    - [Boolean](#boolean)
    - [Integer](#integer)
    - [String](#string)
    - [Addresses](#addresses)

## Basic contract structure
Below an example is given of a simple Solidity smart-contract. Although this contract does not have a lot of practical value, it covers a lot of the core-concepts of a contract written in Solidity. Let's go over it together.

```solidity
pragma solidity ^0.4.0;

contract SimpleStorage {
    uint storedData;

    function set(uint x) public {
        storedData = x;
    }

    function get() public view returns (uint) {
        return storedData;
    }
}
```
### Compiler Version
The firs line `pragma solidity ^0.4.0;` tells the Ethereum Virtual Machine (EVM - the thing that runs our contract) what version of the compiler should be used to compile the contract. This line **must** be included at the very top of every contract we'll be writing. Solidity is a relativily new language and is being developed heavily. This means the language changes quite a lot and the differnences between versions are substantial. Therefore, please make sure the version you specify is the same as shown on the bottom write corner of the [Solidity Documentation](https://solidity.readthedocs.io/).

### Contract Declaration
To declare a contract we use the `contract` keyword followed by the name of the contract followed by two curly braces (`{}`). This name can be anything you wish.

**example**
```solidity
contract MyFirstContract {

}
```

> By convention the contract name is written in PascalCase. This means you capitalize every first letter of a word.

## Variables
In smart-contracts we use variables to store and retreive values. Take the contract above for example. It declares a variable called `storedData` and uses the functions `set()` and `get()` to store and retreive the value (more on functions later).

Variables must be declared along with their 'value type'. A value type tells the EVM what kind of value we want to store and how much memory it should allocate. This could be an integer (a number without a decimal point), a string (a piece of text), an address (belonging to a human or contract) and more.

Variables are declared with the following structure: `<value type> <variable name>`. For example: `uint myAge` tells the EVM we want to store an unsigned integer (`uint`) (a positive, whole number) that we will call `myAge`.

> By convention the contract name is written in camelCase. This means you capitalize every first letter of a word, except for the first word.

### Primitive Value Types
As mentioned before, we need to specify a value type whenever we are declaring a variable. A value type tells the EVM what kind of value we want to store and how much memory is needed to store it.

Let's go over a few common value types.

#### Boolean
The boolean value type can be used to store exactly two kind of values, `true` and `false`.
#### Integer
An integer is a 'whole' number that has no decimal point. There are multiple types of integers, but for now we focus on `signed` and `unsigned` integers. The most important difference between these is that `signed` integer types can hold positive and negative integer values, whereas `unsigned` integers can only hold positive integer values.

#### String
The string type is used to store a piece of text.

#### Addresses
The address type is used to store two kinds of addresses:
  - contract addresses (needed to find and interact with a smart-contract on the blockchain)


