# Course Overview

This Repo contains everything surrounding the educational material for the course in the HU blockchain minor.

## Goals

Practical goal: students can write a simple smart contract in solidity.

Overarching goal: students have gained insight into the potential of smart contracts and several related blockchain subjects. They know about the application and the why of blockchain.

## Practical details

Actual deadline for educational material: 15-08-2020
Proposed deadline: 08-08-2020

Deliverables:

- 7 lessons
- Final assignment
- Grading matrix

Lessons will be 2 hours long, 1 hour of which will be providing a theoretical framework and context surrounding different blockchain topics. The other hour will be practical, based on the [cryptozombies](https://cryptozombies.io/) lessons.

At the end of the course we'll do a feedback session to improve material, improve it and make it open source.

## Lesson structure

### Week 1: Getting started and the basics of Smart Contracts

1. Course Introduction

   - What to expect / learning goals.
   - Where to find course materials.
   - Environment, what do and don't we expect
   - Explanation final assignment / examination.

2. Smart Contracts: the basics

   - What are smart contracts & how do they relate to blockchain
   - How do Smart Contracts work
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

Zombie battle system

- Cryptozombies lesson 4

### 5: ... and 'ERC721 & Crypto-Collectibles'

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

#### Basic

1. Smart contract security
   1. DAO hack

### Week 6 - Testing smart contracts

#### Basic

1. Testing smart contracts with Solidity in Remix IDE

#### Advanced

1. Testing smart contracts in JavaScript with Truffle Suite

### Week 7 - Decentralized Storage

Decentralized File Storage with InterPlanetary File System (IPFS) and Swarm

#### Basic

1. What is IPFS? What is Swarm?
   1. What are the benefits of using decentralized storage?
      1. deduplication, because everything is addressed by a hash
      2. integrity, files match the hash...
      3. ...
2. Download and explore IPFS Desktop
3. Publishing files on IPFS

#### Advanced

1. Make your front-end interface available via IPFS

## Prerequisites

For joining this course a basic knowledge about blockchain is assumed. Programming experience is not required. For the people who have programming experience there is an advanced track.

## Learning Goals

- The student is able to work with the Remix IDE. This includes writing, testing and deploying smart contracts from within Remix.
- The student is able to write and deploy Solidity smart contracts on the Ethereum (test) network. For example smart contracts for coins, voting and bets
- The student is able to connect the Remix IDE to Metamask and manage transactions via Metamask.
- The student is able to describe what Ethereum, Solidity, Remix IDE, MetaMask, InterPlanetary File System (IPFS), Swarm and Self-Sovereign Identity (SSI) are.

### Advanced Learning Goals

- The student is able to work with Truffle Suite. This includes writing, testing and deploying smart conrtracts with Truffle Suite.
- The student is able to create a simple front-end interface that interacts with ethereum smart contracts via Web3.js.
- The student is able to deploy files on IPFS or Swarm. This includes a simple front-end interface that interacts with Ethereum.

## Final Assignment

Each student needs to hand in a final assignment. The final assignment will show that the student has achieved the learning goals described above. The final assignment for the advanced track will build upon the base final assigment.

**Basic**
Create a betting factory contact that allows multiple people to bet on something. This project should involve a minimum of two contracts and should have a test coverage of 80%.

**Advanded**
The advanced assignment is free to choose, but should at least have the following:

- a minimum of two contracts
- a front-end hosted on IPFS/SWARM
- 80% test coverage

## Course Material

There will be a document available for each week with explanations and assignments. Slides will also be made available toghether with a cheatsheet. The cheatsheet will give an overview of difficult topics and will provide some dutch translations to make it easier to understand.

## Resources

- Remix IDE - [https://remix.ethereum.org/](https://remix.ethereum.org/)
- Remix IDE Documentation - [https://remix-ide.readthedocs.io/en/latest/](https://remix-ide.readthedocs.io/en/latest/)
- MetaMask - [https://metamask.io/](https://metamask.io/)
- Truffle Suite - [https://www.trufflesuite.com/](https://www.trufflesuite.com/)
- Web3.js Documentation - [https://web3js.readthedocs.io/en/v1.2.4/](https://web3js.readthedocs.io/en/v1.2.4/)
- Swarm Documentation - [https://swarm-guide.readthedocs.io/en/latest/introduction.html](https://swarm-guide.readthedocs.io/en/latest/introduction.html)
- IPFS - [https://ipfs.io/](https://ipfs.io/)
- IPFS Desktop - [https://docs.ipfs.io/](https://docs.ipfs.io/)
- EthPM Documentation - [https://ethpm.github.io/ethpm-spec/](https://ethpm.github.io/ethpm-spec/)
