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

The Basics of Smart Contracts

---

### Smart Contract Structure

```javascript
// compiler version
pragma solidity ^0.5.2;

// contract declaration
contract CookieStorage {
    // state variable of reference type int
    int private storeProfit;
    // state variable
    struct Cookie{
        string flavor;
        uint price;
        bool available;
    }

    // array
    Cookie[] public trayOfCookies;


    // function to add a cookie to the array
    function addCookie(string memory _flavor, uint _price, bool _available) public {
        Cookie memory c = Cookie(_flavor, _price, _available);
        trayOfCookies.push(c);
    }

    // function to get how many cookies are on the tray
    function getCookieCount() public view returns (uint _cookieCount){
        return trayOfCookies.length;
    }
}
```

---
### Comments
```javascript
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
---
### Compiler version
```solidity
pragma solidity ^0.5.2;
```
- Every contract must have the compiler version specification on top
- Make sure you select a matching compiler version in Remix IDE
- Make sure you select the right version when looking at the Solidity documentation

---
### The Constructor
```javascript
pragma solidity ^0.5.2;

contract Cake {
  // state variable
  string flavor;

  // the constructor creates a cake the first time it is called
  constructor(string memory _flavor) public {
    flavor = _flavor;
  }

  // this function is not a constructor and therefore can be called more than once
  // more about functions later
  function setFlavor(string memory _flavor) public {
     flavor = _flavor;
  }

  // function that returns the flavor of the cake when called
  // more about functions later
  function getFlavor() public view returns (string memory _flavor) {
    return flavor;
  }
}
```

---
### Variables
There are two kinds:
- Value Types (passed by value)
- Reference Types (passed by reference)

---
### Variable declaration
```javascript
string flavor = "chocolate";
int price = 5;
```
Variables do not have to be initialized upon declaration, an example:

```javascript
// this variable is declared here
string flavor;


function setFlavor() public {
    // and assigned a value here
    flavor = "chocolate";
}
```
---
### Value Types
As mentioned before, we need to specify a type whenever we are declaring a variable. A type tells the EVM what kind of value we want to store and how much memory is needed to store it.
| Type      |                                             |   Example                                           |
| ---------------- | ------------------------------------------- | -------------------------------------------- |
| Boolean          | Contains value true or false.               | `bool isEmpty; // false`                     |
|                  |                                             | `bool isEmpty = false; // false`             |
| Signed integer   | Contains positive or negative whole number. | `int degrees = 113;`                         |
|                  |                                             | `int degrees = -20;`                         |
| Unsigned integer | Contains positive whole number              | `int age = 24;`                              |
|                  |                                             | `int age;`                                   |
| String           | Contains text                               | `string message = "Hello World"`             |
|                  |                                             | `string number = "1234" // still text value` |

---
# Reference Types
<!-- _class: invert -->

---
### Structs
Structs can be used to 'group' multiple variables together that form data objects
```javascript
// struct cookie with attributes flavor, price and available.
struct Cookie{
    string flavor;
    uint price;
    bool available;
}

// create specific cookies
Cookie c1 = Cookie("oat", 2, true);
Cookie c2 = Cookie("double chocolate chip", 4, false);

// get specific cookie attributes
c1.available // returns true
c1.flavor // returns "oat"
c2.price // returns 4
```
---
### Arrays (1/2)
An array is a collection or list of multiple variables of the same type
```javascript
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

// adding to the array of structs with push
gifts.push(christmasGift);

// getting the amount of items in the array with length
gifts.length()

// array of ints
int[] arrayOfInts;

// adding to the arrayOfInts with push
arrayOfInts.push(16);
arrayOfInts.push(2);
arrayOfInts.push(2009);
arrayOfInts.push(3);

// variable len is now the same as 4
int len = arrayOfInts.length()

// array of ints with fixed length 20
int[20] fixedArrayOfInts;
```
---
### Arrays (2/2)
```javascript
// array of ints
int[] arrayOfInts;

// adding to the arrayOfInts with push
arrayOfInts.push(16);
arrayOfInts.push(2);
arrayOfInts.push(2009);
arrayOfInts.push(3);

// how to get 2009 from the array
arrayOfInts[2]

// how to save 2009 in the variable year
uint year = arrayOfInts[2]
```
---
### Operators (1/3)
Operators are used to manipulate variables, the most common ones you will probably already know:
- x + y
- x - y
- x \* y
- x / y

---
### Operators (2/3)
However, you might not be familliar with the **exponantial** and **modulo** operators

#### Exponential
The exponential operator calculates `X` to the power of `Y`. Although this is often written as `X^Y` in mathematics, the operator in Solidity is written as \*\*.

```solidity
// Using the exponential operator to calculate bacterial growth
uint startingBacteria = 100
uint hours = 3;

int bacteriaPopulation = startingBacteria ** hours
// the variable bacteriaPopulation has now been assigned the value of 100^3 = 1000000
```

---
### Operators (3/3)
#### Modulo
Modulo is the operator that calculates the remainder of a division. When you divide 14 by 12, the 12 fits once with 2 left over. 14 % 12 = 2. This operator is often used to determine if the result of a division is even.

```solidity
33 % 3 = 0 // no remainder
33 % 5 = 3 // some remainder
```

---
### Functions
- Functions allow a contract to be manipulated
- They can have inputs (parameters or arguments)
- They can return values (return values)
```javascript
    // state variable
    struct Cookie{
        string flavor;
        uint price;
        bool available;
    }

    // array
    Cookie[] public trayOfCookies;

    // function to add a cookie to the array
    function addCookie(string _flavor, uint _price, bool _available) public {
        // creating a new struct cookie (reference types like stuct need to explicitly mention memory, storage or calldata)
        Cookie memory c = Cookie(_flavor, _price, _available);

        // we've seen push() before
        trayOfCookies.push(c);
    }
```

---
<!-- _class: invert -->

# Putting it together 🛠

---
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

        // a new struct
        Cookie memory c = Cookie(_flavor, _price, _available);

        // .push()
        trayOfCookies.push(c);
    }

    // function to get how many cookies are on the tray
    function getCookieCount() public view returns (uint _cookieCount){

        // .length()
        return trayOfCookies.length;
    }
}
```
---
<!-- _class: invert -->
# Any questions?