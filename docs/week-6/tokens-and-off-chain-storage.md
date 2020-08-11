# Week 6: Tokens And Off-Chain Storage

- [Week 6: Tokens And Off-Chain Storage](#week-6-tokens-and-off-chain-storage)
  - [Smart Contracts](#smart-contracts)
  - [Ethereum](#ethereum)
  - [Off-Chain Storage](#off-chain-storage)
    - [IPFS](#ipfs)
    - [Swarm](#swarm)
  - [Solidity](#solidity)
    - [Counters](#counters)
  - [Additional Reading / Watching](#additional-reading--watching)

## Smart Contracts

Generally a token is a representation of something. If you receive a voucher for a free hamburger at MCDonalds that voucher represents the free burger. Your diploma is a representation of the education you've received an you often collect tokens in games as a representation of how well you are doing.

In blockchain a token means the same thing. A representation of something else. Often these representations can be stored or exchanged. This might remind you of previous material where cryptocurrency was discussed. There is however a difference between a cryptographic coin and a token. A cryptographic coin has its own blockchain and can therefore be independent of its platform. A token is on a specific platform and can therefore be used only within that platform.

Cryptocurrency coins are usually only used for payments. Tokens can be used for payments but also for other things. Security tokens are used to represent shares in a company for example and asset tokens are used to represent real world assets like houses.

> From basicattentiontoken.org:
> "The Basic Attention Token can be used to obtain a variety of advertising and attention-based services on the BAT platform, as it is exchanged between publishers, advertisers, and users. The token’s utility is derived from, or denominated by, user attention."

Tokens can be **fungible** or **non-fungible**. A fungible token is exchangeable. If you have one share in a company it doesn't matter which specific share you have. Cryptocurrency coins and money in general is also fungible. It does not matter which specific euro you have, only that you have one euro.

With non-fungible tokens it _does_ matter which specific token you have. They are not interchangeable. One plane ticket is not the same as another plane ticket, although they might look the same.

Non-fungible tokens are used for any case where you might need collectibles. For gamification for example. CryptoKitties is the most known example of this. They created unique cats with a unique digital genetic code, these cats can be bought and traded but they are non-fungible. If you trade one cat for one cat they are different cats with different information and worth. Some CryptoKitties are very rare. Baseball cards (a classic real-world trading example) have also been deployed via blockchain by MLB Crypto Baseball.

## Ethereum

Everyone is allowed to develop applications on Ethereum. Because of this, there need to be rules on how to implement things like tokens or exchanges. These are called standards and this process happens through ERC.

ERC stands for Ethereum Request for Comments. It is a standard, a set of rules, for how something should be done on the Ethereum network. Developers can make an EIP (Ethereum Improvement Proposal) about their ERC to get it accepted by the Ethereum community. Once a standard is accepted everyone can follow the same rules for development which makes everything work together nicely.

The standard for normal tokens is ERC-20. It describes the rules that a token should follow on the Ethereum network in order to work smoothly.

To create non-fungible tokens on Ethereum the ERC-721 standard is used. This standard describes the rules non-fungible tokens should follow when managed, owned and traded. The standard contains a minimal interface with functions that need to be implemented. A developer can choose to add additional functionality.

```solidity
pragma solidity ^0.4.20;

        /// @title ERC-721 Non-Fungible Token Standard
        /// @dev See https://github.com/ethereum/EIPs/blob/master/EIPS/eip-721.md

        interface ERC721 /* is ERC165 */ {
            event Transfer(address indexed _from, address indexed _to, uint256 indexed _tokenId);

            event Approval(address indexed _owner, address indexed _approved, uint256 indexed _tokenId);

            event ApprovalForAll(address indexed _owner, address indexed _operator, bool _approved);

            function balanceOf(address _owner) external view returns (uint256);

            function ownerOf(uint256 _tokenId) external view returns (address);

            function safeTransferFrom(address _from, address _to, uint256 _tokenId, bytes data) external payable;

            function safeTransferFrom(address _from, address _to, uint256 _tokenId) external payable;

            function transferFrom(address _from, address _to, uint256 _tokenId) external payable;

            function approve(address _approved, uint256 _tokenId) external payable;

            function isApprovedForAll(address _owner, address _operator) external view returns (bool);
        }

        interface ERC165 {
            function supportsInterface(bytes4 interfaceID) external view returns (bool);
        }

        interface ERC721TokenReceiver {
            function onERC721Received(address _operator, address _from, uint256 _tokenId, bytes _data) external returns(bytes4);
         }
```

As previously discussed, a well designed interface allows you to implement these exact functions in your own smart contract code.

## Off-Chain Storage

As mentioned often, determining what should and should not be stored on a blockchain is very important. Only things that need to be immutable need to be stored on-chain. In a lot of use cases there is still a need for data storage however. Some interesting decentralized ways of doing this are discussed.

### IPFS

The InterPlanetary File System (IPFS) is a network for storing and sharing data. It is very similar to BitTorrent as it consists of a decentralized peer-to-peer system. Users can upload and download content. DApps combining Ethereum and IPFS can solve a lot of problems that blockchain has re. storing data. The actual data is stored on IPFS, while hashes of the data are stored on Ethereum to provide immutability. Remix IDE even has built in functionality to publish on IPFS.

![IPFS Workings](assets/ipfs-woorking.png)

[IPFS](https://ipfs.io/#how)

### Swarm

Swarm is also a peer-to-peer distributed storage platform, it is a layer on Ethereum that allows users to store and share data in a decentralized way. Remix IDE has built in functionality to publish on Swarm.

[Swarm](https://ethersphere.github.io/swarm-home/)

## Solidity

### Counters

Counters are a general coding principle. They are used to keep count of something.

They work by initializing a variable which then gets changed upwards using `++` or downwards using `--`.

```solidity
contract Bus {
    int public passengers = 0;

    function leaveBus() public {
        passengers--;
    }

    function getOnBus() public{
        passengers++;
    }
}
```

## Additional Reading / Watching

[Ethereum and IPFS](https://medium.com/pinata/ethereum-and-ipfs-e816e12a3c59)
