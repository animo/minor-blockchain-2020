# Summary

This summary bundles some of the material that is spread out over several lessons.

## Types Overview

### Value Types

| Value Types      |                                             |                                                                                                  |
| ---------------- | ------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| Type             |                                             | Example                                                                                          |
| Boolean          | Contains value true or false.               | `bool isEmpty; // false`                                                                         |
|                  |                                             | `bool isEmpty = false; // false`                                                                 |
| Signed integer   | Contains positive or negative whole number. | `int degrees = 113;`                                                                             |
|                  |                                             | `int degrees = -20;`                                                                             |
| Unsigned integer | Contains positive whole number              | `int age = 24;`                                                                                  |
|                  |                                             | `int age;`                                                                                       |
| String           | Contains text                               | `string message = "Hello World"`                                                                 |
|                  |                                             | `string number = "1234" // still text value`                                                     |
| Address          | Contains an account address                 | `address myAddress = 0x111122223333444455556666777788889999AAAABBBBCCCCDDDDEEEEFFFFCCCC`         |
|                  |                                             | `address payable myAddress = 0x111122223333444455556666777788889999AAAABBBBCCCCDDDDEEEEFFFFCCCC` |

### Reference Types

| Reference Types |                                                    |                                             |
| --------------- | -------------------------------------------------- | ------------------------------------------- |
| Type            |                                                    | Example                                     |
| Struct          | Contains custom type that groups variables         | `struct Person { uint age; string name; }`  |
| Array           | Contains other variables, is typed same as content | `int[] ages; // array of int`               |
|                 |                                                    | `Person[] people // array of struct Person` |

## Visibility

| Visibility Modifiers |                                                                                                                                       |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Type                 |                                                                                                                                       |
| Public               | Function and variable can be called from all potential parties. Is default.                                                           |
| Private              | Function and variable can be called only from within the contract it is defined in.                                                   |
| Internal             | Function can be called from within the contract it is defined in AND from within derived contracts (which inherit the main contract). |
| External             | Function can only be called from a third party. Not from the main contract and not from a derived contract.                           |

## Function Type Modifiers

| Function Type Modifiers |                                                                                  |
| ----------------------- | -------------------------------------------------------------------------------- |
| Type                    |                                                                                  |
| Pure                    | Indicates that function does not change or use any data from the contract.       |
| View                    | Indicates that function does not change but **does** use data from the contract. |
| Payable                 | Indicates that the function can receive Ether.                                   |
