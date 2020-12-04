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

/* img[alt~="center"] {
  display: block;
  margin: 0 auto;
} */

</style>

# Decentralized Development

Protecting your contract

---

# Topics of the day

- Require statement
- Modifiers
- Inheritance

---

# Require

`require()` is a special function in Solidity that enables you to easily protect the functions in your code.

It works like this:

- You give the function a **condition**
- If the condition fails (is **false**), the execution is terminated and the funds are returned to the caller.
- If the condition succeeds (is **true**), the execution is continued
- You can optionally pass a message (a string) to send back to the user if the condition fails

---

# Example

```javascript
function onlyMoreThan1Ether() public payable {
  require(msg.value >= 1 ether);
  // this code is only reached if at least 1 Ether was sent
}
```

---

# Example with message

```javascript
function onlyMoreThan1Ether() public payable {
  require(msg.value >= 1 ether, "You need to send at least 1 ether to call this function");
  // this code is only reached if at least 1 Ether was sent
}
```

---

# Let's try it

```javascript
pragma solidity 0.4.25;

contract RequireExample {
    address private creator;
    event MyMessage(string functionName);


    constructor() public {
        creator = msg.sender;
    }

    function onlyCreator() public {
        require(msg.sender == creator, "You are not allowed to call this function");
        emit MyMessage("onlyCreator");
    }

    function onlyMoreThan1Ether() public payable {
        require(msg.value >= 1 ether, "You need to send at least 1 ether to call this function");
        emit MyMessage("onlyMoreThan1Ether");
    }

    function onlyOver18(uint age) public {
        require(age >= 18, "You need to be over 18 to call this function");
        emit MyMessage("onlyMoreThan1Ether");
    }
}

```

---

# Modifiers

The modifier keyword can be used to create functions that **guard** other functions. In a modifier function **you can decide to run, or not to run** another function.

That sounds funky, but it's actually quite easy!

> Let's have a look

---

# Modifier example

```javascript
pragma solidity 0.4.25;

contract ModifierExample {
    address private creator;
    event MyMessage(string functionName);

    constructor() public {
        creator = msg.sender;
    }

    modifier onlyCreator() {
        if (msg.sender == creator) {
          emit MyMessage("withoutModifier");
          _; // this executes the 'other' function
        }
    }

    function withoutModifier() public {
      if (msg.sender == creator) {
          emit MyMessage("withoutModifier");
        }
    }

    function withModifier() public onlyCreator {
        emit MyMessage("withModifier");
    }
}
```

---

# Modifier example with `require()`

As we've seen in the previous example, the function seems to **succeed** while the function actually **did not** execute. This is why you should to combine modifiers with `require`.

```javascript
pragma solidity 0.4.25;

contract ModifierExample {
    address private creator;
    event MyMessage(string functionName);

    constructor() public {
        creator = msg.sender;
    }

    modifier onlyCreator() {
      require(msg.sender == creator, "You are not allowed to call this function");
      _; // this executes the 'other' function
    }

    function funcWithModifier() public onlyCreator {
        emit MyMessage("withModifier");
    }
}
```

---

# Inheritance

Inheritance is used to **inherit** code from other contracts. It is used to **avoid duplicate code**, as well as to **improve security**.

Think of it like this:

- A BMW 8 Series is a car
- A car has wheels
- Therefore, a BMW 8 Series has wheels

> In other words: **a BMW 8 Series _inherently_ has the properties of a car (wheels, engine, seats, etc.)**

---

# Inheritance in contracts

In Solidity, you can use inheritance to give a contract the properties and functions of another contract. This enables you to **reduce the amount of duplicate code** if two contracts require the same functionality. It also increases security because **less coding means less mistakes**.

---

<!-- _header: 'Source: https://www.tutorialspoint.com/solidity/solidity_function_modifiers.htm' -->

# Inheritance example(1/4)

```javascript
pragma solidity ^0.5.0;

contract Ownable {
   address owner;
   constructor() public {
      owner = msg.sender;
   }
   modifier onlyOwner {
      require(msg.sender == owner);
      _;
   }
}

contract CakeStore is Ownable {
   uint public cakePrice;
    uint private balance;

   constructor(uint _cakePrice) public {
      cakePrice = _cakePrice;
      balance = 0;
   }

   modifier priced(uint amount) {
    uint totalPrice = (cakePrice * amount);
    require(msg.value >= totalPrice, "PAY MORE");
    _;
   }

   function setCakePrice(uint price) public onlyOwner {
      cakePrice = price;
   }

   function buyCake(uint amount) public payable priced(amount) returns(string memory) {
     // protect
     uint totalPrice = (cakePrice * amount);
     require(msg.value >= totalPrice, "PAY MORE");

     balance += msg.value;
     return "Here is/are your cookie(s)";
   }
}
```

---

<!-- _header: 'Source: https://www.tutorialspoint.com/solidity/solidity_function_modifiers.htm' -->

# Inheritance example (2/4)

```javascript
pragma solidity ^0.5.0;

contract Ownable {
   address owner;
   constructor() public {
      owner = msg.sender;
   }
   modifier onlyOwner {
      require(msg.sender == owner);
      _;
   }
}

contract CakeStore is Ownable {
   uint public cakePrice;
    uint private balance;

   constructor(uint _cakePrice) public {
      cakePrice = _cakePrice;
      balance = 0;
   }

   modifier priced(uint amount) {
    uint totalPrice = (cakePrice * amount);
    require(msg.value >= totalPrice, "PAY MORE");
    _;
   }

   function setCakePrice(uint price) public onlyOwner {
     cakePrice = price;
   }

   function buyCake(uint amount) public payable priced(amount) returns(string memory) {
     balance += msg.value;
     return "Here is/are your cookie(s)";
   }
}
```

---

# Inheritance example (3/4)

```javascript
pragma solidity ^0.5.0;

contract Ownable {
   address owner;
   constructor() public {
      owner = msg.sender;
   }
   modifier onlyOwner {
      require(msg.sender == owner);
      _;
   }
}

contract Priceable is Ownable {
    uint price;

    constructor(uint _price) public {
        price = _price;
    }

    modifier priced(uint amount) {
      uint totalPrice = (price * amount);
      require(msg.value >= totalPrice, "PAY MORE");
      _;
   }


    function setPrice(uint _price) public onlyOwner {
      price = _price;
   }

}


contract CakeStore is Priceable {
    uint private balance;

   constructor() public {
      balance = 0;
   }

   function buyCake(uint amount) public payable priced(amount) returns(string memory) {
     balance += msg.value;

     return "Here is/are your cookie(s)";
   }
}

```

---

# Inheritance example (4/4)

```javascript
pragma solidity ^0.5.0;

contract Ownable {
   address owner;
   constructor() public {
      owner = msg.sender;
   }
   modifier onlyOwner {
      require(msg.sender == owner);
      _;
   }
}

contract Priceable is Ownable {
    uint price;

    constructor(uint _price) public {
        price = _price;
    }

    modifier priced(uint amount) {
      uint totalPrice = (price * amount);
      require(msg.value >= totalPrice, "PAY MORE");
      _;
   }

    function setPrice(uint _price) public onlyOwner {
      price = _price;
   }

}


contract HasBalance {
    uint private balance;

    constructor() public {
        balance = 0;
    }

    function addToBalance(uint amount) internal {
        balance += amount;
    }
}

contract Buyable is HasBalance, Priceable {

    function buy(uint amount) public payable priced(amount) returns(string memory) {
     uint totalPrice = amount * price;

     addToBalance(totalPrice);

     // return any leftover funds (if any)
     msg.sender.transfer(msg.value - totalPrice);

     return "Here is/are your cookie(s)";
   }

}


contract CakeStore is Buyable {
    uint private balance;

   constructor() public {
      balance = 0;
   }
}

```

---

<!-- _class: invert -->

# Any questions?
