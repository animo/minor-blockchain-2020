# Course Overview

This repo contains everything surrounding the educational material for the decentralised development course in the HU blockchain minor.

## Prerequisites

For joining this course a basic knowledge about blockchain is assumed. Programming experience is not required.

## Goals

Practical goal: students can write a simple smart contract in solidity.

Overarching goal: students have gained insight into the potential of smart contracts and several related blockchain subjects. They know about the application and the why of blockchain.

After this course:

- The student is able to work with the Remix IDE. This includes writing, testing and deploying smart contracts from within Remix.
- The student is able to write and deploy Solidity smart contracts on the Ethereum (test) network. For example smart contracts for coins, voting and bets
- The student is able to connect the Remix IDE to Metamask and manage transactions via Metamask.
- The student is able to describe what Ethereum, Solidity, Remix IDE, MetaMask, InterPlanetary File System (IPFS), Swarm and Self-Sovereign Identity (SSI) are.

## Course Material

During the course the student will follow [CryptoZombies](https://cryptozombies.io/en/solidity) lessons 'Solidity Path: Beginner to Intermediate Smart Contracts'. Each week relevant concepts to the CryptoZobies lesson will be explained using live coding examples. In addition to this material several important decentralized technologies and concepts will be explained.

## Final Assignment

Each student needs to hand in a final assignment. The final assignment will show that the student has achieved the learning goals described above. The assignment will be graded according to the provided matrix.

<!-- TODO Add matrix -->

Assignment
Create a betting factory contact that allows multiple people to bet on something. This project should involve a minimum of two contracts.

<!-- There will be a document available for each week with explanations and assignments. Slides will also be made available toghether with a cheatsheet. The cheatsheet will give an overview of difficult topics and will provide some dutch translations to make it easier to understand. -->

## Practical details

Actual deadline for educational material: 15-08-2020
Proposed deadline: 08-08-2020

Deliverables:

- 7 lessons
- Final assignment
- Grading matrix

Lessons will be 2 hours long.

At the end of the course we'll do a feedback session to improve material, improve it and make it open source.

## Lesson structure

### Week 1: Getting started and the basics of smart contracts

1. Course Introduction

   - What to expect / learning goals.
   - Where to find course materials.
   - Environment, what do and don't we expect
   - Explanation final assignment / examination.

2. Smart Contracts: the basics

   - What are smart contracts & how do they relate to blockchain
   - How do Smart Contracts work
   - Ethereum: the basics
   - Solidity: the basics and a cheat sheet
     - operators (include modulo)
     - uint & int & string & typecasting
     - variables
     - structs & arrays (include public, getters)
     - hash function
     - function declarations
       - Memory storage
       - public / private
       - return values
       - modifiers (view/pure)
     - events
   - Show a smart contract on remix ide

3. Making the Zombie Factory
   - Cryptozombies lesson 1

### Week 2: Expanding the world by interacting with other contracts and blockchains

1. Smart Contracts in the real world

   - Benefits
   - Use cases / industries

2. Ethereum: accounts & ether

3. Solidity: interaction w other contracts and blockchains
   <!-- A contract will just sit on the blockchain doing nothing until someone calls one of its functions. So there will always be a msg.sender. -->

   - Mappings & addresses (addition to structs and arrays)
   - functions 2: return of the functions
     - if statement (+else)
     - global variables -> msg.sender
     - require
     - storage and memory (structs and arrays in functions)
     - internal & external visibility
   - Imports
   - Inheritance
   - Interface: looks, use, purpose

4. Zombies attack their victims
   - Cryptozombies lesson 2

### 3: Security and financing transactions

1. Immutability
2. Gas & gas cost & saving gas (view functions, structs, storage)
3. Using other contracts
4. Backdoors
5. Functions 3: functions revenge

   - modifiers (also with arguments)
   - structs as arguments

6. Time
7. For loops
8. Advanced Solidity Concepts
   - Cryptozombies lesson 3

### 4: Money money money

1. payable -> require money for functionality and withdraw
2. random nums

3. Zombie battle system
   - Cryptozombies lesson 4

### 5: Tokens

1. ERC721
2. Multiple inheritance
3.

ERC721 & Crypto-Collectibles

- Cryptozombies lesson 5

### 6: ... and 'App Front-ends & Web3.js'

### 7: ...

---

### Week 2 - Decentralized Applications, Remix IDE and Smart Contracts

Introduction to Decentralized Applications.

1. What are decetralized applications?
   - How do they differ from a 'normal' application?

### Week 3

### Week 4

### Week 5

<!-- #### Basic

1. Smart contract security
   1. DAO hack

Decentralized File Storage with InterPlanetary File System (IPFS) and Swarm

#### Basic

1. What is IPFS? What is Swarm?
   1. What are the benefits of using decentralized storage?
      1. deduplication, because everything is addressed by a hash
      2. integrity, files match the hash...
      3. ...
2. Download and explore IPFS Desktop
3. Publishing files on IPFS -->

<!-- ## Resources

- Remix IDE - [https://remix.ethereum.org/](https://remix.ethereum.org/)
- Remix IDE Documentation - [https://remix-ide.readthedocs.io/en/latest/](https://remix-ide.readthedocs.io/en/latest/)
- MetaMask - [https://metamask.io/](https://metamask.io/)
- Truffle Suite - [https://www.trufflesuite.com/](https://www.trufflesuite.com/)
- Web3.js Documentation - [https://web3js.readthedocs.io/en/v1.2.4/](https://web3js.readthedocs.io/en/v1.2.4/)
- Swarm Documentation - [https://swarm-guide.readthedocs.io/en/latest/introduction.html](https://swarm-guide.readthedocs.io/en/latest/introduction.html)
- IPFS - [https://ipfs.io/](https://ipfs.io/)
- IPFS Desktop - [https://docs.ipfs.io/](https://docs.ipfs.io/)
- EthPM Documentation - [https://ethpm.github.io/ethpm-spec/](https://ethpm.github.io/ethpm-spec/) -->
