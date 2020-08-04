# Week 1: Getting Started With The Basics Of Smart Contracts

<!-- TODO:
- fix visibility part, gifs don't really add anything, functions and variables are explained together as one. Getter setter not well explained.
       - Memory storage
       - return values
     - events -->

## Decentralized Development

Development of applications generally consists of two parts, front-end development and back-end development. The front-end is what the user sees and interacts with, the back-end contains all the business logic and data storage.

> When you login to a website, the username/password form and the button with the function that sends the login information would be classified as 'front-end'. The website's logic of how to validate the information once it's received and what to send back is classified as 'back-end'. How the information that is send back is then presented (think succes or error messaging) is part of the front-end.

Decentralized applications (or **dApps**) are applications whos back-end code runs on a decentralized network instead of centralized servers. These apps are not dependant on or controlled by a single entity. There is no single point of failure and trust can be generated through technology instead of middlemen or authority.

Although the term dApp is now almost always used to describe applications that make use of a blockchain network, this is not a necessity. Apps that use the BitTorrent protocol like Popcorn Time or uTorrent are also dApps, as they run on a decentralized p2p network.

Blockchain-based dApps are applications that communicate with a blockchain. The front-end works (largely) the same as with a centralized application but the business logic about what needs to happen with sent information is stored in the form of **smart contracts** on a blockchain. In this course we'll discuss the specifics that come with developing these types of decentralized applications and learn how to write smart contracts for real world use cases.

## Smart Contracts: The Basics

Smart contracts are basically digital contracts that automatically enforce their content. They can be used to replace complicated structures that we currently use to guarantee that an agreement is upheld.

Imagine you and a friend decide to bet on the outcome of a sports match. You think team A will win, your friend thinks team B will win. The loser has to pay up €100,-. If you and your friend completely trust each other you might just shake on it and leave it at that. However, what happens if you do not trust your friend to actually follow through and pay up the €100,- once team B (in your mind inevitably) loses? You might ask an impartial friend to function as a **trusted third party**. You could both give him €100,- to hand over €200,- to the winner once the match is over. Trust problem solved! Except it isn't. The trusted third party could turn out not to be as trustworthy as you hoped, be robbed or simply lose the money. Once you start worrying about this you might escalate the contstruction further, by involving a lawyer or a bank. Smart contracts fix the ever growing complexity of trust problems when agreements are made.

In a smart contract the rules for the agreement are written in executable code. Once the triggers for the agreement are activated, the consequenses are immediately and automatically carried out. Because the smart contract is written in code that is publically available on the blockchain there is **transparancy** while the individuals involved can be **anonymous**. Because the smart contract cannot be changed once on the blockchain there is **immutability**. These factors combined with the fact that the blockchain itself cannot be altered by a central authority but is **distributed** eliminate the need for a trusted third party or middleman.

> In the example of your sports bet, you and your friend could write your agreement in the form of a smart contract on the Ethereum network. This smart contract could (for example) require €100,- from both of you to check the outcome online and route €200,- directly to the winner. Trust problem solved! This time for real.

Smart contracts have many practical uses. They can be made for any agreement that follows if-this-then-that logic. The more incentive anyone has to commit fraud, the more useful the smart contract becomes. For example think about the consequences implementing smart contracts would have for voting, financial services, renting a house, insurance cases, digital identity, trading etc. Because smart contracts can be used to create a transparent, immutable, decentralized and automated proces they can also be very cost-effective as a result of their efficiency.

So smart contracts are pieces of executable code on a blockchain network. What does that mean? In the next section we'll examine where the code 'lives' and how the actual proces of triggering the smart contract works.

## Ethereum: The Basics

Next time you and that friend you don't trust decide on a bet, you might want to try using a smart contract to handle the execution. But you would need a blockchain network to put it to ensure it has all those great immutable, decentralized and transparent qualities you want. There are different options for what blockchain to use, including setting up your own, however currently for dApps the most widely used network is Ethereum.

If you visit ethereum.org you will find that _"Ethereum is a global, open-source platform for decentralized applications."_ You can use the established Ethereum network to put your smart contract and use existing nodes to validate and update information. Because a blockchain depends on the computational power of the network these nodes are rewarded for participating through digital currency. In the Ethereum network this currency is called Ether. In next weeks material we will go into more detail about how this actually works.

Smart contracts, once put on the Ethereum network have an address. This address is used to find the correct smart contract and send the required information. Just like an e-mail address (or regular address) is used to find the person you sent information to. The information that is sent to the smart contract is called a transaction.

## Solidity

Solidity is a programming language for writing smart contracts on Ethereum and other blockchain platforms. It is what we'll be learning during this course. We'll start with the basics and work our way up. If at any point you want to try out some code at home or in class you can navigate to https://remix.ethereum.org/ to create a contract file and compile it.

If you have never programmed before it can be intimidating to get started. Solidity has excellent [documentation](https://solidity.readthedocs.io/) but the documentation assumes you have some basic programming experience. In this course manual the main concepts will be explained for people completely new to programming, with references to the original documentation for additional information.

> Do: Go back and forward between this material and the CryptoZombies lesson, occasionally adding Google if something is unclear. \
> Do Not: Read through all of the documentation and expect to understand it completely and all at once before starting the CryptoZombies material.

### Basic contract structure

Below an example is given of a simple Solidity smart contract. Although this contract does not have a lot of practical value, it covers a lot of the core concepts of a contract written in Solidity. Let's go over it together.

```solidity
pragma solidity ^0.4.0;

contract AgeStorage {
    uint age;

    function set(uint newAge) public {
        age = newAge;
    }

    function get() public view returns (uint) {
        return age;
    }
}
```

#### Compiler Version

The first line `pragma solidity ^0.4.0;` tells the compiler what version of the compiler must be used to compile the contract. A compiler is a computer program that transforms computer code written in one programming language (the source language) into another programming language (the target language). Ethereum smart contracts are run in the Ethereum Virtual Machine (EVM). The EVM doesn't understand Solidity code, it only understands EVM code. So to deploy our smart contracts to the Ethereum network we must first make sure to compile our Solidity code into EVM code.

This line **must** be included at the very top of every contract we'll be writing. Solidity is a relatively new language and is being developed heavily. This means the language changes quite a lot and the differences between versions are substantial. Therefore, please make sure the version you specify is the same as shown on the bottom left corner of the [Solidity Documentation]

```solidity
pragma solidity ^0.5.2;
```

- [Solidity Docs - Version Pragma]

#### Contract Declaration

To declare a contract we use the `contract` keyword followed by the name of the contract followed by two curly braces (`{}`). This name can be anything you wish.

```solidity
contract AgeStorage {

}
```

> By convention the contract name is written in PascalCase. This means you capitalize every first letter of a word.

### Variables

In smart contracts we use variables to store and retrieve values. Take the `AgeStorage` contract above for example. It declares a variable called `age` and uses the functions `set()` and `get()` to store and retrieve the age (more on functions later).

Variables must be declared along with their 'type'. A type tells the EVM what kind of value we want to store and how much memory it should allocate. This could be an integer (a number without a decimal point), a string (a piece of text), an address (belonging to a human or contract) and more.

Variables are declared with the following structure: `<variable type> <variable name> = <variable value>`. See the example below, it tells the EVM we want to store an integer (`int`) that we will call `age` and give it a value of `17`.

```solidity
int age = 17;
```

It is not required for values to be assigned a value on initialization. You can set the value at a later moment. This can be useful if you don't know the value at the moment of declaration.

```solidity
int age;

age = 17;
```

> By convention a variable is written in camelCase. This means you capitalize every first letter of a word, except for the first word. Programmers use this to increase readability of variables. It is also recommended to keep your variable names short and descriptive. It might be tempting to name your variables x and y but other people won't be able to understand what's going on (and neither will you if you return to your code in a few months).

#### Types

As mentioned before, we need to specify a type whenever we are declaring a variable. A type tells the EVM what kind of value we want to store and how much memory is needed to store it.

Let's go over a few common types.

- [Solidity Docs - Types]

##### Boolean

The boolean type can be used to store exactly two kind of values, `true` and `false`. A boolean is indicated by the `bool` keyword.

```solidity
bool canBuyAlcohol = false;
bool canBuyPlants = true;
```

- [Solidity Docs - Boolean]

##### Integer

An integer is a 'whole' number that has no decimal point. There are multiple types of integers, but for now we focus on `signed` and `unsigned` integers. The most important difference between these is that `signed` integer types can hold positive and negative integer values, whereas `unsigned` integers can only hold positive integer values.

If we want to declare a variable for age it is logical to take make it an `unsigned` integer as an age can never be below 0.

```solidity
// Signed integer, can be positive and negative
int negativeAge = -17;

// Unsigned Integer, can only be positive
uint age = 17;
```

- [Solidity Docs - Integer]

##### String

The string type is used to store a piece of text. It can contain any value you like.

```solidity
string myText = "Hello World!";
```

- [Solidity Docs - String]

##### Address

The address type is used to store an ethereum account addresses. Ethereum has two types of accounts:

- Normal externally controlled accounts
- Contract accounts

```solidity
address myAddress = 0x2bE37643B3Ecb05c4C2Ec646534b3f053565716A;
```

- [Solidity Docs - Address]
- [Ethereum Account Types]

##### Structs

Structs are for when you need to make your own type that groups multiple variables.

```solidity
// example with assigned variables
struct Gift {
    uint price = 30.99;
    uint grams = 500;
    string birthdayGreeting = "Enjoy this gift, happy birthday dad!";
}

// example with unassigned variables
struct Gift {
    uint price;
    uint grams;
    string birthdayGreeting;

}
```

- [Solidity Docs - Structs]

#### Operators

Operators are a way to manipulate variables. You know most of these already. They are the regular math operators:

- x + y
- x - y
- x \* y
- x / y

Two operators you might not know are **exponential** and **modulo**.

##### Exponential

The exponential operator calculates X to the power of Y. Although this is often written as X^Y in mathematics, the operator when coding is actually \*\*.

```solidity
// Using the exponential operator to calculate bacterial growth
uint startingBacteria = 100
uint hours = 3;

int bacteriaPopulation = startingBacteria ** hours
// the variable bacteriaPopulation has now been assigned the value of 100^3 = 1000000
```

##### Modulo

Modulo is the operator that calculates the remainder of a devision. When you devide 14 by 12, the 12 fits once with 2 left over. 14 % 12 = 2. This operator is often used to determine if the result of a division is even.

```solidity
33 % 3 = 0 // no remainder
33 % 5 = 3 // some remainder
```

#### Arrays

Variables can be stored in arrays. An array is a collection of things.

```solidity
// struct
struct Gift {
    uint price;
    uint grams;
    string birthdayGreeting;
}

// array of structs;
Gift[] public gifts;

// create a new Gift
Gift christmasGift = Gift(90, 1100, "Merry Christmas");

// adding to the array of structs
gifts.push(christmasGift)

// array of ints
int[] arrayOfInts;

// adding to the arrayOfInts
arrayOfInts.push(16)
```

### Comments

Comments are a great way to describe the meaning of code. In the examples before we already used some comments. The compiler will remove any comments during compilation, so it doesn't add anything to the code itself. It just helps the next person that is going to work on the contract, which probably will be you.

```solidity
// Single-line comment, everything on this line is a comment.

/*
Multi-line comment,
everything is a comment
until you end the comment
*/

uint age = 17; // Comments can also be written on lines with code

/*
This next line is also a comment, so no variable is declared
uint age = 17;
*/
```

- [Solidity Docs - Comments]

### Functions

Functions are the executable units of code within a contract. Functions can be executed after which the code inside it will be run.

A function is declared with the following syntax:

```solidity
function <functionName>(<parameters>) <visibility> <function type> <modifiers> <return variables> {
    <function code>
}
```

A function **must** always be declared inside a contract. It is not possible to declare a function outside of a contract. So the function should be defined between the curly brackets (`{}`) of the contract.

If we take the `AgeStorage` contract as an example.

```solidity
contract AgeStorage {
    uint age;

    function set(uint newAge) public {
        age = newAge;
    }

    function get() public view returns (uint) {
        return age;
    }
}
```

for the `set()` function:

- **`set`** is the **function name**
- **`uint newAge`** are the **parameters**
- **`public`** is the **visibility**
- the function has **no function type**
- the function has **no modifiers**
- the function has **no return variables**
- **`age = newAge;`** is the **function code**

for the `get()` function:

- **`get`** is the **function name**
- the function has **no parameters**
- **`public`** is the **visibility**
- **`view`** is the **function type**
- the function has **no modifiers**
- **`returns (uint)`** are the **return variables**
- **`return age;`** is the **function code**

So what do the `parameters`, `visibility`, `function type`, `modifiers` and `return variables` actually mean? Let's go over all of them.

> By convention a function name is written in camelCase. This means you capitalize every first letter of a word, except for the first word.

- [Solidity Docs - Functions]

#### Parameters

Parameters are the input values of a function. Let's say we want to create a function that calculates the sum of two integer values. Parameters allow us to pass the two integer values to the function so the sum can be calculated.

In the example below two parameters, `val1` and `val2` are declared as parameters for the `sum` function. Parameters are declared the same way as variables, so every parameter should have a type. In this case `uint`.

Now whenever we want to execute the `sum` function, which we are going to do in later lessons, we are required to pass the two parameters to the `sum` function.

```solidity
function sum(uint val1, uint val2) public pure returns (uint) {
    return val1 + val2;
}
```

- [Solidity Docs - Function Parameters]

#### Visibility

The visibility of a function specifies the accessibility of the function when you or another function wants to interact with it.

There are four types of visibility:

- `public`
- `private`
- `external`
- `internal`

At the moment we'll handle public and private visibility. Internal and external visibility can be found in the next chapter.

- [Solidity Docs - Visibility]

##### Public

Public functions and state variables are the most open visibility type. The function and variable can be accessed from inside and outside of the contract. It is important to be careful with public functions, as they allow anyone to call the function.

For public state variables, an automatic getter function is generated. A getter function is a function that simply returns the value of a variable. For the public `age` variable in the example below an `age()` function is generated that will return the value of `age`. This way we don't have to define the function to get the value of `age` ourselves.

```solidity
contract AgeStorage {
    uint public age;

    // We dont have to define a function get because it is automatically generated.

    function set(uint newAge) public {
        age = newAge;
    }
}
```

![Visibility Public](./assets/visibility-public.gif)

#### Return Variables

TODO

- [Solidity Docs - Return Variables]

#### Memory

TODO

##### Private

Private functions and state variables are the most closed visibility type. They can only be accessed from other functions inside of the contract.

```solidity
contract AgeStorage {
    uint private age;

    function set(uint newAge) private {
        age = newAge;
    }
}
```

![Visibility Private](./assets/visibility-private.png)

#### Modifiers

Functions can serve many different goals in Solidity. We use function modifiers if these goals need to be clarified.

- [Solidity Docs - Function Modifiers]

##### Pure

Sometimes a function does not change any data or even use any data from the contract. For example if you have written a function to add two numbers that you give it as parameters and return the result. This is called a **pure** function.

```solidity
function sum(uint val1, uint val2) public pure returns (uint) {
    return val1 + val2;
}
```

- [Solidity Docs - Pure Functions]

##### View

If the function does not change anything, but does read data from the contract, it is a **view** function.

```solidity
uint age = 17;

function doubleTheAge(uint memory age) public view returns (uint) {
    return age * 2
}
```

- [Solidity Docs - View Functions]

### Events

TODO

### Resources

- [Solidity Documentation]
- [Solidity Docs - Version Pragma]
- [Solidity Docs - Types]
- [Solidity Docs - Boolean]
- [Solidity Docs - Integer]
- [Solidity Docs - String]
- [Solidity Docs - Address]
- [Ethereum Account Types]
- [Solidity Docs - Comments]
- [Solidity Docs - Structs]
- [Solidity Docs - Functions]
- [Solidity Docs - Function Parameters]
- [Solidity Docs - Return Variables]
- [Solidity Docs - Visibility]
- [Solidity Docs - Function Modifiers]
- [Solidity Docs - View Functions]
- [Solidity Docs - Pure Functions]

<!-- Internal links -->

[solidity documentation]: https://solidity.readthedocs.io/
[solidity docs - version pragma]: https://solidity.readthedocs.io/en/latest/layout-of-source-files.html#version-pragma
[solidity docs - types]: https://solidity.readthedocs.io/en/latest/types.html
[solidity docs - boolean]: https://solidity.readthedocs.io/en/latest/types.html#booleans
[solidity docs - integer]: https://solidity.readthedocs.io/en/latest/types.html#integers
[solidity docs - string]: https://solidity.readthedocs.io/en/latest/types.html#bytes-and-strings-as-arrays
[solidity docs - address]: https://solidity.readthedocs.io/en/latest/types.html#address
[ethereum account types]: https://ethereum.gitbooks.io/frontier-guide/account_types.html
[solidity docs - comments]: https://solidity.readthedocs.io/en/latest/layout-of-source-files.html#comments
[solidity docs - structs]: https://solidity.readthedocs.io/en/v0.5.3/structure-of-a-contract.html#struct-types
[solidity docs - functions]: https://solidity.readthedocs.io/en/latest/contracts.html#functions
[solidity docs - function parameters]: https://solidity.readthedocs.io/en/latest/contracts.html#function-parameters
[solidity docs - return variables]: https://solidity.readthedocs.io/en/latest/contracts.html#return-variables
[solidity docs - visibility]: https://solidity.readthedocs.io/en/latest/contracts.html#visibility-and-getters
[solidity docs - function modifiers]: https://solidity.readthedocs.io/en/latest/contracts.html#function-modifiers
[solidity docs - view functions]: https://solidity.readthedocs.io/en/latest/contracts.html#view-functions
[solidity docs - pure functions]: https://solidity.readthedocs.io/en/latest/contracts.html#pure-functions
