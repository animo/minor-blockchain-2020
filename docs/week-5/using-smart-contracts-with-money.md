# Week 5: Using Smart Contracts With Money

## Smart Contracts

A lot of the use cases for smart contracts involve money. An automatic money transfer.......

- Insurance
- Banking

Crytocurrency

## Ethereum

On Ethereum there are different types of account. Externally owned accounts (EOAs) for users of the network and contract accounts for smart contracts. Both these types of account can store money in the form of the Ethereum cryptocurrency **Ether** (ETH).

Previously we've discussed how ETH is used to pay for Gas to execute operations. Since ETH is a cryptocurrency it can also be transferred as a form of payment seperate from the payment needed for miners to validate the network. When a money transfer is a part of a smart contract use case, sending and receiving ETH between accounts is a way to implement this.

Although an account can store some ETH on its own most EOA and smart contract accounts use a **wallet**. A wallet is a type of smart contract specifically for receiving, storing and spending money. It has its own address and keys and needs to be deployed to the ethereum network by an account.

Just like other smart contracts it costs Gas to create a wallet (as it costs Gas to deploy a smart contract). The owner of the wallet then uses it to store their ETH and, when needed, spend or receive it.

> Remember, a wallet _is_ a smart contract but can also be _used_ by other smart contracts.

A wallet works largely the same for EOAs as it does for smart contracts. Although smart contract wallets often have more functionality.

TODO: Software, hardware wallet https://blog.gnosis.pm/breaking-down-ethereum-wallets-options-2162b41477d7

TODO: Keys and wallets, restoring, etc.

## Solidity

### Functions

To move around money using smart contracts there need to be functions to pay, check and withdraw money from a contract. EOA wallets with a user interface already have these functions implemented. There are default aspects of solidity to assist with this.

#### address.transfer(amount)

The .transfer() function allows you to send an amount to an address of your choosing.

```solidity
// transfer to address
customer.transfer(0.100);

// withdraw money yourself
function withdraw() external onlyOwner {
    msg.sender.transfer(0.100);
}

// allow others to withdraw money
function withdraw() external {
    msg.sender.transfer(0.100);
}
```

#### Payable Modifier

The payable modifier allows functions to receive Ether.

If we think back to the betting example, a payable function could be used to collect a certain amount of money for participants to be allowed to participate.

A function can simply be payable without additional context. But often it is combined with requirements, checks or restrictions. For example the execution of a payable function can be dependent on payement. To do this you can use the require function to require a certain value to be sent with the activating call. So far we have mostly used the call data to check the msg.sender, but there is a lot of other available information.

```solidity
contract BettingContract {


    function payToEnter() external payable {
    // remember the special variable 'msg.value'
    require(msg.value == 0.30 ether);
    addToParticipants(msg.sender)
    }
}
```
