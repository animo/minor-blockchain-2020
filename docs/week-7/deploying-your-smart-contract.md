# Deploying to Ethereum Testnet

- [Deploying to Ethereum Testnet](#deploying-to-ethereum-testnet)
  - [Ethereum: Testnet vs. Mainnet](#ethereum-testnet-vs-mainnet)
  - [Deployment tutorial](#deployment-tutorial)
    - [Remix IDE](#remix-ide)
    - [Connecting MetaMask](#connecting-metamask)

## Ethereum: Testnet vs. Mainnet

As you might be sick of hearing right now smart contract code, once deployed, can not be changed. In week 2 the benefits of this were discussed, in week 4 the security risks and costs involved and now, in week 7, we are almost at a point where you will deploy your own smart contract code.

As many other dApp developers before you, you might be hesitant about doing this. If deploying smart contract code is such a big deal, maybe imperfect code shouldn't be deployed without thoroughly testing it.

For this exact reason testnets exist. Testnets are copies of the Ethereum blockchain that are identical in almost every way. The Ether in these networks however is worthless. This makes them ideal for testing out your imperfect code before deploying to mainnet Ethereum.

If you're working on some top-secret billion dollar idea you might use a **private test network**. This network is basically your own personal blockchain that you can use to test smart contract code and interact with wallets and transactions. If keeping things private is not a major concern you can also use a **public test network**. These are available to anything and everyone. You might remember from week 5 that you created a MetaMask wallet account, which you put 1 Ether on. The "Ropsten Test Network" that you used to do this is a public test network.

> The only real difference between the Ropsten Test Network and the Ethereum Main Network is the _agreement_ that its Ether is worthless.

Although Ether is worthless in test networks, it still needs to exist. To try out transactions from a wallet to your code you will need to pay for those transactions. The way test networks solve this is through faucets. The Ropsten Faucet 'drips' 1 Ether every 5 seconds, you can request this Ether by giving you testnet account address.

To test your smart contract code you will need to have a wallet to send transactions. Your MetaMask wallet is excellently suited for this purpose.

## Deployment tutorial

### Remix IDE

So far we have used Remix IDE in class to show examples of smart contract code and to check for errors. However, Remix IDE is useful for a lot more than just checking your code. You can use it to deploy the contracts you've written.

### Connecting MetaMask

In week 5 you made a MetaMask wallet account and received 1 Ether. This week we are using MetaMask to interact with smart contract code.

Navigate to your MetaMask account (or redo the steps from week 5 to make a new one).

> As you can see on the MetaMask account page, you can choose between multiple Ethereum networks. By default, MetaMask will try to connect to the main network. The other choices are public testnets, any Ethereum node of your choice, or nodes running private blockchains on your own computer.

> We are going to use the "Ropsten Test Network". The ropsten network is almost the same as the main network, except that it is meant for testing. In the ropsten network Ether has no value and there's no guarantee your data will stay on the network.

// TODO continue
