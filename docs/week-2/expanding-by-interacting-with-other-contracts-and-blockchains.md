# Week 2: Expanding By Interacting With Other Contracts And Blockchains

## Ethereum: Accounts, Gas And Ether

https://medium.com/sunnya97/understanding-ether-vs-gas-82ce2f1dc560#:~:text=Ether%20is%20a%20currency.&text=with%20oil%20arises.-,Ethereum%20could%20have%20implemented%20Gas%20as%20a%20separate%20token%20from,or%20anything%20else%20for%20gas.

On chain.
address of a smart contract
send your transaction to the address.
transaction includes gas and function / data.
contract receives transaction, uses gas to execute the function you sent.

It does not cost gas to read information. Only to change the chain.

Look at blockexplorer
Ethereum is....

Because of this it is the most used blockchain-based dApps platform.

### Functions

#### Visibility

We already discussed private and public visibility.
//TODO

##### Internal

```solidity
contract AgeStorage {
    uint internal age;

    function set(uint newAge) internal {
        age = newAge;
    }
}
```

![Visibility Internal](./assets/visibility-internal.png)

##### External

```solidity
contract AgeStorage {
    // Not allowed
    // uint external age;

    function set(uint newAge) external {
    }
}
```

![Visibility External](./assets/visibility-external.gif)
