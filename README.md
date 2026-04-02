# Arc Testnet Deployment Guide

## What Are We Building?
Deploy HelloArc.sol on Arc Testnet. Stores and retrieves a greeting message.

## Environment Setup
Mac: Terminal
Windows: Ubuntu WSL (8GB RAM, 512GB storage)

## Install Foundry & Initialize Project
curl -L foundry.paradigm.xyz | bash
foundryup
forge init arc-deploy
cd arc-deploy

## Smart Contract: HelloArc.sol
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract HelloArc {
    string public greeting;

    constructor(string memory _greeting) {
        greeting = _greeting;
    }

    function setGreeting(string memory _greeting) public {
        greeting = _greeting;
    }

    function getGreeting() public view returns (string memory) {
        return greeting;
    }
}
```

## Compile
forge build

## Wallet Setup
cast wallet new
PRIVATE_KEY="your_private_key"

## Fund Wallet
Go to faucet.circle.com and request testnet USDC.

## Deploy Contract
forge create src/HelloArc.sol:HelloArc --constructor-args "hello arc" --rpc-url $ARC_TESTNET_RPC_URL --private-key $PRIVATE_KEY --broadcast

## Interact
cast call <CONTRACT_ADDRESS> "getGreeting()(string)" --rpc-url $ARC_TESTNET_RPC_URL

## Troubleshooting & Notes
- Experimental deployment; no guaranteed rewards.
- Save your source code locally.

