# Week 2: Storage And Getting Into Functions

## Smart contracts

// immutability explained further

Smart contracts are pieces of code that are deployed on a blockchain network and that automatically enforce their content.

## Ethereum: Storage

Previously we briefly mentioned how contract code is stored on the Ethereum network. Smart contracts, once put on the Ethereum network have an address, which is used to find the correct smart contract and send the required information.

When we say the code is stored on the network, we mean it is stored on the decentalized open source blockchain. ...

## Solidity: The Basics

Lets take another look at the CookieStorage contract example.

```solidity
// compiler version
pragma solidity ^0.5.2;

// contract declaration
contract CookieStorage {
    // state variable of reference type struct
    struct Cookie{
        string flavor;
        uint price;
        bool available;
    }

    // array of structs
    Cookie[] public trayOfCookies;


    // function to add a cookie to the array
    function addCookie(string memory _flavor, uint _price, bool _available) public {
        // creating a new struct
        Cookie memory c = Cookie(_flavor, _price, _available);
        // using .push() to add to the array
        trayOfCookies.push(c);
    }

    // function to get how many cookies are on the tray
    function getCookieCount() public view returns (uint _cookieCount){
        // using .length() for the length of the array
        return trayOfCookies.length;
    }
}
```

In week one we discussed the structure of the contract and we discussed variables, types and arrays. This week we're diving a bit deeper into actually making some changes, using **functions**.

### Functions

[Solidity Docs - Functions]

Functions are the executable units of code within a contract. Functions can be executed (or _called_) after which the code inside it will run.

A function is declared with the following syntax:

```solidity
function <functionName>(<parameters>) <visibility modifier> <other modifiers> <return variables> {
    <function code>
}
```

A function **must** always be declared inside a contract. It is not possible to declare a function outside of a contract. So the function should be defined between the curly brackets (`{}`) of the contract.

If we take the functions from `CookieStorage` contract as an example.

```solidity
function addCookie(string memory _flavor, uint _price, bool _available) public {
    Cookie memory c = Cookie(_flavor, _price, _available);
    trayOfCookies.push(c);
}

function getCookieCount() public view returns (uint _cookieCount){
    return trayOfCookies.length;
}
```

for the `addCookie()` function:

- **`addCookie`** is the **function name**
- **`string _flavor`, `uint _price` and `bool _available`** are the **function parameters**
- **`public`** is the **visibility modifier**
- the function has no **state modifier**
- the function has **no other modifiers**
- the function has **no return variables**
- **`Cookie memory c = Cookie(_flavor, _price, _available); trayOfCookies.push(c);`** is the **function code**

for the `getCookieCount()` function:

- **`getCookieCount`** is the **function name**
- the function has **no function parameters**
- **`public`** is the **visibility modifier**
- **`view`** is the **state modifier**
- the function has **no other modifiers**
- **`returns (uint _cookieCount)`** are the **return variables**
- **`return trayOfCookies.length;`** is the **function code**

So what do the `parameters`, `visibility`, `modifiers` and `return variables` actually mean? Let's go over all of them.

> By convention a function name is written in camelCase. This means you capitalize every first letter of a word, except for the first word.

#### Parameters

[Solidity Docs - Function Parameters]

Parameters are the input values of a function. Let's say we want to create a function that calculates the sum of two integer values. Parameters allow us to pass the two integer values to the function so the sum can be calculated (using the operator `+`).

In the example below two parameters, `val1` and `val2` are declared as parameters for the `sum` function. Parameters are declared the same way as variables, so every parameter should have a type. In this case `uint`.

Now whenever we want to execute the `sum` function, which we are going to do in later lessons, we are required to pass the two parameters to the `sum` function.

```solidity
function sum(uint _val1, uint _val2) public pure returns (uint) {
    return _val1 + _val2;
}
```

> You might have noticed that all the variables that are used inside of a function have an underscore before their name (\_val1). This is not necessary but a coding convention. Just like camelCase for a function name is convention. It serves to create more readable code for everyone.

The function `addCookie` from the CookieStorage contract takes parameters for flavor, price and availability. The function then uses these parameters within the function to create a new Cookie struct.

```solidity
//parameters are input for the function
function addCookie(string memory _flavor, uint _price, bool _available) public {

    // parameters are used in the function
    Cookie memory c = Cookie(_flavor, _price, _available);
    trayOfCookies.push(c);
}
```

#### Storage and memory

In week 1 we briefly mentioned that reference types (remember **structs** and **arrays**), when used in functions, need to explicitly say where they are stored. Any variable saved in storage is saved permanently on the blockchain, while anything saved in memory is saved temporarily and forgotten after the action that needs it is finished.

```solidity
function addCookie(string memory _flavor, uint _price, bool _available) public {

    // because the Cookie c is a temporary variable that does not need to be stored on the blockchain right now, it gets the memory keyword
    Cookie memory c = Cookie(_flavor, _price, _available);
    trayOfCookies.push(c);
}
```

You can also use the memory keyword with arrays, to create a new array inside a function without needing to write anything to storage. The array will then only exist until the end of the function call.

The way we can mostly tell the difference (for now) is that storage variables (state variables) are defined outside of functions, while memory variables are defined within functions.

```solidity
pragma solidity ^0.5.2;

contract Cake {
  // state variable gets saved in storage
  string flavor;

  function newAge(uint _age) public pure returns (uint){

      //the variable _year is stored in memory, it is used and forgotten as soon as the function is over
      uint _year = 1;

      return _age + _year;

  }
}
```

Remember, because this example does not use reference types like `struct` or `array` storage and memory are implicit. If we did use reference types we would have to explicitly state storage or memory like in `addCookie()`.

#### Visibility Modifiers

[Solidity Docs - Visibility]

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

##### Public

Public functions and state variables are the most open visibility type. The function and variable can be accessed from inside and outside of the contract. It is important to be careful with public functions, as they allow anyone to call the function.

For public state variables, an automatic **getter function** is generated. A getter function is a function that simply returns the value of a variable. For the public `age` variable in the example below an `age()` function is generated that will return the value of `age`. This way we don't have to define the function to get the value of `age` ourselves.

```solidity
contract AgeStorage {
    uint public age;

    // We don't have to define a function to get the value for because it is automatically generated. We know its name is age()

    function setAge(uint _newAge) public {
        age = _newAge;
    }
}
```

![Visibility Public](./assets/visibility-public.gif)

##### Private

Private is the most closed visibility type. Functions or variables with this visibility can only be accessed from other functions inside of the contract. It is generally recommended to keep functions private unless more visibility is needed.

```solidity
contract AgeStorage {

    // age can only be accessed from within the AgeStorage contract
    uint private age;

    function set(uint newAge) private {
        age = newAge;
    }

}
```

![Visibility Private](./assets/visibility-private.png)

#### Return Variables

[Solidity Docs - Return Variables]

Functions can be used to execute an operation without changing anything. However functions are often used to return some information through return variables. The function needs to announce beforehand that it returns something as well as the type of what it returns. The function will then return what comes after the **return** keyword.

```solidity
contract MyContract {

    // this function returns a uint
    function doubleTheAge(int age) private returns (uint){
        return age * 2
    }

}
```

#### State Modifiers

[Solidity Docs - Function Modifiers]

Function modifiers are used to modify the behavior of functions. They create additional features or make sure there are restrictions on a function. State modifiers say something about how the function interacts with the blockchain.

##### Pure

[Solidity Docs - Pure Functions]

Sometimes a function does not change any data or even use any data from the contract. For example if you have written a function to add two numbers that you give it as parameters and return the result. This is called a **pure** function.

```solidity
function sum(uint val1, uint val2) public pure returns (uint) {
    return val1 + val2;
}
```

##### View

[Solidity Docs - View Functions]

If the function does not change anything, but does read data from the contract, it is a **view** function. The function is read only.

```solidity
uint age = 17;

function doubleTheAge(uint memory age) public view returns (uint) {
    return age * 2
}
```

Or in our `CookieStorage` example.

```solidity
// function to get how many cookies are on the tray
function getCookieCount() public view returns (uint _cookieCount){
    // using .length() for the length of the array
    return trayOfCookies.length;
}
```

### Events

[Solidity Docs - Events]

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

### Additional reading / watching

<!-- Internal Links -->

[solidity docs - functions]: https://solidity.readthedocs.io/en/latest/contracts.html#functions
[solidity docs - function parameters]: https://solidity.readthedocs.io/en/latest/contracts.html#function-parameters
[solidity docs - return variables]: https://solidity.readthedocs.io/en/latest/contracts.html#return-variables
[solidity docs - visibility]: https://solidity.readthedocs.io/en/latest/contracts.html#visibility-and-getters
[solidity docs - function modifiers]: https://solidity.readthedocs.io/en/latest/contracts.html#function-modifiers
[solidity docs - view functions]: https://solidity.readthedocs.io/en/latest/contracts.html#view-functions
[solidity docs - pure functions]: https://solidity.readthedocs.io/en/latest/contracts.html#pure-functions
[solidity docs - events]: https://solidity.readthedocs.io/en/develop/contracts.html#events
