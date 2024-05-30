# FundMe Solidity Contract

This repository contains the Solidity smart contract for a decentralized funding platform called FundMe. The platform allows users to contribute funds in ETH, which are then managed by the contract owner. The contract integrates Chainlink's price feeds to ensure contributions meet a minimum USD value.

## Table of Contents
- [FundMe Solidity Contract](#fundme-solidity-contract)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Features](#features)
  - [Contract Details](#contract-details)
    - [FundMe Contract](#fundme-contract)
      - [Key Functions](#key-functions)
    - [PriceConverter Library](#priceconverter-library)
      - [Key Functions](#key-functions-1)
  - [Getting Started](#getting-started)
    - [Prerequisites](#prerequisites)
    - [Installation](#installation)
- [Compilation](#compilation)
- [Usage](#usage)
    - [Funding the Contract](#funding-the-contract)
    - [Withdrawing Funds](#withdrawing-funds)
- [Deployment](#deployment)
- [Testing](#testing)
- [Test Coverage](#test-coverage)

## Overview

FundMe is a smart contract that allows users to send ETH, which is then converted to USD using Chainlink price feeds to ensure contributions meet a minimum threshold. Only the contract owner can withdraw the funds.

## Features

- Users can fund the contract with ETH.
- Ensures minimum funding amount based on USD value.
- Contract owner can withdraw funds.
- Integrates with Chainlink price feeds for ETH/USD conversion.

## Contract Details

### FundMe Contract

The `FundMe` contract is the core of this project. It includes the following key functionalities:

- **Funding:** Users can send ETH to the contract. The amount must meet a minimum USD value.
- **Withdrawal:** Only the contract owner can withdraw all funds.
- **Price Feeds:** Uses Chainlink's `AggregatorV3Interface` to fetch the current ETH/USD price.

#### Key Functions

- `fund()`: Allows users to fund the contract.
- `withdraw()`: Allows the contract owner to withdraw funds.
- `cheaperWithdraw()`: Optimized version of the withdraw function for lower gas costs.
- `getVersion()`: Returns the version of the price feed.
- `getAddressToAmountFunded(address)`: Returns the amount funded by a specific address.
- `getFunder(uint256)`: Returns the address of a funder by index.
- `getOwner()`: Returns the owner of the contract.

### PriceConverter Library

The `PriceConverter` library provides utilities to convert ETH amounts to USD using Chainlink price feeds.

#### Key Functions

- `getPrice(AggregatorV3Interface)`: Returns the current ETH price in USD.
- `getConversionRate(uint256, AggregatorV3Interface)`: Converts an ETH amount to USD.

## Getting Started

### Prerequisites

- [Foundry](https://getfoundry.sh/)
- [Solidity](https://docs.soliditylang.org/)

### Installation

Clone the repository and install dependencies:

```bash
git clone https://github.com/your-repo/fundme.git
cd fundme
```
# Compilation

Compile the smart contracts using Foundry:
```bash
forge build
```
# Usage
### Funding the Contract
Users can fund the contract by sending ETH. Ensure the amount meets the minimum USD value specified. Originally it is 5 USD.
### Withdrawing Funds
Only the contract owner can withdraw the funds. This can be done using the withdraw() or cheaperWithdraw() functions.

# Deployment
Deploy the contract using the included deployment script:

```bash
forge script script/DeployFundMe.s.sol
```

# Testing
There are 4 test tiers.
1. Unit
2. Integration
3. Forked
4. Staging

This repo cover #1 and #3.

Tests are included to ensure the contract functions as expected. Run the tests using Foundry:
```bash
forge test
```
or
```bash
// Only run test functions matching the specified regex pattern.

"forge test -m testFunctionName" is deprecated. Please use 

forge test --match-test testFunctionName
```
or
```bash
forge test --fork-url $SEPOLIA_RPC_URL
```

# Test Coverage

```bash
forge coverage
```