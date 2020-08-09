# Week 2: Storage and Functions

## Smart contracts

// immutability explained further

Smart contracts are pieces of code that are deployed on a blockchain network and that automatically enforce their content.

## Ethereum: Storage

// How does 'storing' code and values on ethereum work.

## Solidity: The Basics

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

#### Storage and memory

// TODO fix

Any variable saved in storage is saved permanently on the blockchain, while anything saved in memory is saved temporarily and forgotten after the action that needs it is finished.

The way we can mostly tell the difference is that storage variables are defined outside of functions, while memory variables are defined within functions.

// TODO expand

You can use the memory keyword with arrays to create a new array inside a function without needing to write anything to storage. The array will only exist until the end of the function call

#### Visibility Modifiers

Function modifiers are used to modify the behavior of functions. They create additional features or make sure there are restrictions on a function. Visibility modifiers say something about the accessibility of the function when you or another function wants to interact with it (who is the function visible for).

```solidity
contract MyContract {

    function myFunction () [visibility-here] {
        // do something
    }

}
```

There are four types of visibility:

- `public`
- `private`
- `external`
- `internal`

At the moment we'll handle public and private visibility. Internal and external visibility can be found in next weeks material.

- [Solidity Docs - Visibility]

##### Public

Public functions and state variables are the most open visibility type. The function and variable can be accessed from inside and outside of the contract. It is important to be careful with public functions, as they allow anyone to call the function.

TODO

For public state variables, an automatic **getter function** is generated. A getter function is a function that simply returns the value of a variable. For the public `age` variable in the example below an `age()` function is generated that will return the value of `age`. This way we don't have to define the function to get the value of `age` ourselves.

```solidity
contract AgeStorage {
    uint public age;

    // We dont have to define a function get because it is automatically generated. We know its name is age()

    function set(uint newAge) public {
        age = newAge;
    }
}
```

![Visibility Public](./assets/visibility-public.gif)

##### Private

Private is the most closed visibility type. Functions or variables with this visibility can only be accessed from other functions inside of the contract. It is generally reccomended to keep functions private unless more visibiltiy is needed.

TODO

```solidity
contract AgeStorage {
    uint private age;

    function set(uint newAge) private {
        age = newAge;
    }
}
```

![Visibility Private](./assets/visibility-private.png)

#### Return Variables

Functions can be used to execute an operation without changing anything. However functions are often used to return some information through return variables. The function will return what comes after the **return** keyword.

```solidity
contract MyContract {

    function doubleTheAge(int age) private returns (uint){
        return age * 2
    }

}
```

- [Solidity Docs - Return Variables]

#### State Modifiers

Function modifiers are used to modify the behavior of functions. They create additional features or make sure there are restrictions on a function. State modifiers say something about how the function interacts with the blockchain.

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

If the function does not change anything, but does read data from the contract, it is a **view** function. The function is read only.

```solidity
uint age = 17;

function doubleTheAge(uint memory age) public view returns (uint) {
    return age * 2
}
```

- [Solidity Docs - View Functions]

### Events

Everything that we have been coding so far in solidity has been 'back-end' material. The smart contract lives on the blockchain and that is where all the code is executed and stored. However, if you are building an app for people to use it will need to have a frontend.

Events are the way the frontend is notified for things that are happening in the smart contract. Events are 'fired' in the back-end code and can be 'listened' for in the front-end code. This is how communication between the two works.

```solidity
contract Result {
   // create the event
   event WinnerKnown(address winner, uint amount);

   function determineWinner(address[] memory participants) public  {
       // code to determine the winner from the participants

      // fire the event
      emit Deposit(winner, 100000);
   }
}
```

- [Solidity Docs - Events]

## Recourses

- [Solidity Docs - Functions]
- [Solidity Docs - Function Parameters]
- [Solidity Docs - Return Variables]
- [Solidity Docs - Visibility]
- [Solidity Docs - Function Modifiers]
- [Solidity Docs - View Functions]
- [Solidity Docs - Pure Functions]

<!-- Internal Links -->

[solidity docs - functions]: https://solidity.readthedocs.io/en/latest/contracts.html#functions
[solidity docs - function parameters]: https://solidity.readthedocs.io/en/latest/contracts.html#function-parameters
[solidity docs - return variables]: https://solidity.readthedocs.io/en/latest/contracts.html#return-variables
[solidity docs - visibility]: https://solidity.readthedocs.io/en/latest/contracts.html#visibility-and-getters
[solidity docs - function modifiers]: https://solidity.readthedocs.io/en/latest/contracts.html#function-modifiers
[solidity docs - view functions]: https://solidity.readthedocs.io/en/latest/contracts.html#view-functions
[solidity docs - pure functions]: https://solidity.readthedocs.io/en/latest/contracts.html#pure-functions
[solidity docs - events]: https://solidity.readthedocs.io/en/develop/contracts.html#events