<!--
    author: Timo Glastra <timo@glastra.me>
    edited: 2019-12-17
    notes:
     - Ganache v2.1.2
     - Truffle v5.1.4 (core: 5.1.4)
     - Solidity v0.5.12 (solc-js)
     - Node v12.13.0
     - Web3.js v1.2.1
-->

# Truffle Suite <!-- omit in toc -->

- [Truffle Suite](#truffle-suite)
- [Ganache](#ganache)
- [Truffle](#truffle)
  - [Truffle Setup](#truffle-setup)
  - [Project Structure](#project-structure)
    - [Contracts](#contracts)
    - [Migrations](#migrations)
    - [Tests](#tests)
    - [Config](#config)
- [Code Editor](#code-editor)
- [Sources](#sources)

## Truffle Suite

This week you will start to work with the Truffle Suite. The Truffle Suite is a set of tools that make Ethereum smart contract development easier and more robust.

The suite contains three main components:

- **[Truffle]**: a development environment that helps developers write, test and deploy smart contracts.
- **[Ganache]**: a tool to easily setup a local development blockchain that we'll use to develop and test our smart contracts.
- **[Drizzle]**: a set of front-end libraries that helps us interact with smart contracts.

## Ganache

Ganache is part of the truffle suite and described as a 'one click blockchain'. It allows you to quickly fire up a personal Ethereum blockchain which you can use during development. To get started, download the latest version of [Ganache]. Open the downloaded executable and follow the installation instructions appropriate to your operating system.

<img src="./assets/truffle-startup.png" width="400">
<img src="./assets/truffle-workspace.png" width="400">

When you open Ganache it will ask you to create a workspace, we are going to use the 'QUICKSTART' workspace. You now have a working Ethereum blockchain running on your computer. We are going to use this blockchain whenever we are developing smart contracts, so make sure Ganache is running whenever you are working on this project.

Curious about what Ganache can do? See the [Ganache Docs]

## Truffle

Next we are going to set up a truffle project. Truffle is a JavaScript framework for developing decentralized ethereum applications.

### Truffle Setup

Make sure you have [NodeJS] v8.9.4 or later installed. If you haven't, go to the [NodeJS] page and install the recommended node version.

Run the following commands in Terminal (macOS and Linux) or Command Prompt (Windows):

```bash
node --version # should be v8.9.4 or higher

npm install -g truffle # install truffle with npm

mkdir truffle-project # create empty directory named 'truffle-project'
cd truffle-project # go into 'truffle-project' directory

truffle init # initialize truffle project inside 'truffle-project' directory
```

Example run on macOS:
[![demo](https://asciinema.org/a/j3ZswKE6VkZbjcZfxikKclU9g.svg)](https://asciinema.org/a/j3ZswKE6VkZbjcZfxikKclU9g?autoplay=1)

### Project Structure

You now have a truffle project with the following structure:

```sh
.
├── contracts/ # Directory for Solidity contracts
├── migrations/ # Directory for deployment files
├── test/ # Directory for test files for testing your application and contracts
└── truffle-config.js # Truffle configuration file
```

#### Contracts

All of your contracts are located in your project's `contracts/` directory. As contracts are written in [Solidity][solidity docs], all files containing contracts will have a file extension of `.sol`.

On initialization only a `Migrations.sol` is created. This file contains a `Migration` contract that keeps track of previous deployments. This way you never deploy any contracts that you already deployed.

See [Truffle - Compiling Contracts] for more information.

#### Migrations

Migrations are JavaScript files that help you deploy contracts to the Ethereum network. These files are responsible for staging your deployment tasks, and they're written under the assumption that your deployment needs will change over time. As your project evolves, you'll create new migration scripts to further this evolution on the blockchain. A history of previously run migrations is recorded on-chain through the Migrations contract, described before.

Migrations are placed in the `migrations/` directory. On initialization only a `1_initial_migration.js` is created to deploy deploy the `Migration` contract. In upcoming lessons we will dive deeper into migrations and create one ourself.

See [Truffle - Running Migrations] for more information.

#### Tests

Truffle comes standard with an automated testing framework to make testing your contracts a breeze. This framework lets you write simple and manageable tests in two different ways:

- In JavaScript and TypeScript, for exercising your contracts from the outside world, just like your application.
- In Solidity, for exercising your contracts in advanced, bare-to-the-metal scenarios.

Tests are placed in the `tests/` directory. No tests are created on initialization. After we have spend some time creating contracts we will dive deeper into testing these contracts. For now the `tests/` directory can stay empty.

See [Truffle - Testing Contracts] for more information.

#### Config

The last file in the project is the `truffle-config.js` file. This file is a Javascript file and can execute any code necessary to create your truffle configuration.

When we are going to deploy our written contracts to a live Ethereum test network we will need to change this configuration file to point truffle to the correct network. For development all default values are enough to get started.

See [Truffle - Configuration] for more information.

## Code Editor

> TODO: Recommend Visual Studio Code

## Sources

- [Truffle Suite]
- [Ganache]
- [Ganache Docs]
- [Truffle]
- [Truffle Docs]
- [Drizzle]
- [NodeJS]
- [Solidity Docs]
- [Truffle - Compiling Contracts]
- [Truffle - Running Migrations]
- [Truffle - Testing Contracts]
- [Truffle - Configuration]

<!-- Internal links -->

[truffle suite]: https://www.trufflesuite.com/
[ganache]: https://www.trufflesuite.com/ganache
[ganache docs]: https://www.trufflesuite.com/docs/ganache/overview
[truffle]: https://www.trufflesuite.com/truffle
[truffle docs]: https://www.trufflesuite.com/docs/truffle/overview
[drizzle]: https://www.trufflesuite.com/drizzle
[nodejs]: https://nodejs.org/en/
[solidity docs]: https://solidity.readthedocs.io/en/latest/
[truffle - compiling contracts]: https://www.trufflesuite.com/docs/truffle/getting-started/compiling-contracts
[truffle - running migrations]: https://www.trufflesuite.com/docs/truffle/getting-started/running-migrations
[truffle - testing contracts]: https://www.trufflesuite.com/docs/truffle/testing/testing-your-contracts
[truffle - configuration]: https://www.trufflesuite.com/docs/truffle/reference/configuration
