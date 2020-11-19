---
marp: true
theme: default
_class: invert
---

<style scoped>
table {
    height: 100%;
    width: 100%;
    font-size: 20px;
    color: red;
}
th {
    color: blue;
}
</style>

# Decentralized Development

Storage & Getting Into Functions

---

# Recap

```javascript
// compiler version
pragma solidity ^0.5.2;

// contract declaration
contract CookieStorage {
    // state variable of reference type int
    int private storeProfit;
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

---

# Function structure

```javascript
function <functionName>(<parameters>) <visibility modifier> <other modifiers> <return variables> {
    <function code>
}
```

---

# An example

```javascript
function addCookie(string memory _flavor, uint _price, bool _available) public {
    // creating a new struct
    Cookie memory c = Cookie(_flavor, _price, _available);
    // using .push() to add to the array
    trayOfCookies.push(c);
    }
```

- **`addCookie`** is the **function name**
- **`string _flavor`, `uint _price` and `bool _available`** are the **function parameters**
- **`public`** is the **visibility modifier**
- the function has no **state modifier**
- the function has **no other modifiers**
- the function has **no return variables**
- **`Cookie memory c = Cookie(_flavor, _price, _available); trayOfCookies.push(c);`** is the **function code**

---

# Return values

> Functions can be used to execute an operation without changing anything. However functions are often used to return some information through return variables. The function needs to announce beforehand that it returns something as well as the type of what it returns. The function will then return what comes after the \*_returns_ keyword.

```javascript
pragma solidity ^0.5.17;

contract MyContract {
    // this function returns a uint
    function doubleTheAge(uint age) public pure returns (uint) {
        return age * 2;
    }

}
```

---

# Named return values

```javascript
pragma solidity ^0.5.17;

contract MyContract {
    // this function returns a uint
    function doubleTheAge(uint age) public pure returns (uint myNamedVariable) {
        return age * 2;
    }
}
```

---

# Storage and memory with reference types

As mentioned last week, when we use **reference types**, we need to specify if this is a _storage_ or _memory_ variable.

### The difference

- Storage variables are stored on the ledger
- Memory variables are not, they are gone as soon as the function has completed its execution

---

# An example

```javascript
pragma solidity ^0.5.17;

contract MyContract {
    struct Cookie{
        string flavor;
        uint price;
        bool available;
    }

    // array of structs
    Cookie[] public trayOfCookies;

    function addCookie(string memory _flavor, uint _price, bool _available) public {
        // because the Cookie c is a temporary variable that does not need to be stored on the blockchain right now, it gets the memory keyword
        Cookie memory c = Cookie(_flavor, _price, _available);
        trayOfCookies.push(c);
    }
}
```

---

# MORE EXAMPLES

```javascript
pragma solidity ^0.5.2;

contract Cake {
  // state variable gets saved in storage
  string flavor;

  // _flavor is forgotten as soon as the function call is gone
  function setFlavor(string memory _flavor) public {
      flavor = _flavor;
  }

  function birthdayCandle(uint _age) public pure returns (uint){
      //the variables _year and _age are stored in memory, it is used and forgotten as soon as the function is over
      uint _year = 1;

      return _age + _year;

  }
}
```

---

# Visibility modifiers

> Function modifiers are used to modify the behavior of functions (and even variables!). They create additional features or make sure there are restrictions on a function. Visibility modifiers say something about the accessibility of the function when you or another function wants to interact with it (who is the function visible for).

There are four types of visibility modifiers (we'll only focus on _public_ and _private_ for now):

- `public` (default visibility, accessible outside of the contract)
- `private` (only accessible within the contract)
- `external`
- `internal`

---

# Visability example with functions

```javascript
pragma solidity ^0.5.2;

contract PublicVsPrivate {

    function aVerySexyPublicFunc() public pure returns (string memory myReturnValue) {
        string memory returnValue = "I'm public baby!";
        return returnValue;
    }

    function aVerySexyPrivateFunc() private pure returns (string memory myReturnValue) {
        return "I need privacy...";
    }
}
```

---

# Visability example with variables

```javascript
pragma solidity ^0.5.2;

contract AgeStorage {
    uint public age;

    // We don't have to define a function to get the value for because it is automatically generated. We know its name is age()

    function setAge(uint _newAge) public {
        age = _newAge;
    }
}
```

---

# Function type modifiers

> Function modifiers are used to modify the behavior of functions. They create additional features or make sure there are restrictions on a function. Function type modifiers say something about how the function interacts with the blockchain.

#### There are two types:

- Pure (cannot read from the state/storage, can only do calculations based on the parameters)
- View (does not change the state/storage, but can read and return from it)

Declaring a function to be **view** or **pure** promises that it will not modify the state. As a result these function calls (or transactions) are gas free!

---

# A pure V.S. view function example

```javascript
pragma solidity ^0.5.17;

contract MyContract {
    string myString;

    function setMyString(string memory _myString) public {
        myString = _myString;
    }

    // this function is pure, so it cannot read from the state (e.g. myString)
    function myPureFunction(uint someInt, uint anotherInt) public pure returns (uint) {
        return someInt + anotherInt;
    }

    // this function is view, so it CAN read from the state (but not write to it)
    function myViewFunction() public view returns (string memory) {
        return myString;
    }
}
```

---

# Events

> Everything that we have been coding so far in solidity has been 'back-end' material. The smart contract lives on the blockchain and that is where all the code is executed and stored. However, if you are building an app for people to use it will need to have a frontend.

Events are a way to let 'programs' outside of the blockchain know about what is happening. This may be a frontend to your app, an oracle your contract depends on, or any other piece of software. These 'programs' listen for events that are defined and emitted by the smart-contract.

---

# Example

```javascript

   // create the event
   event CookiesDone(Cookie typeOfCookie, uint amount);

   function bakingCookie(Cookie typeOfCookie) public {

       uint roomInOven = 100
        // baking timer code
        // fire the event
          emit CookiesDone(typeOfCookie, roomInOven);

}
```

---

<!-- _class: invert -->

# Any questions?
