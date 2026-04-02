# Arc Testnet Deployment Guide

## What Are We Building?
Deploy HelloArc.sol on Arc Testnet. Stores and retrieves a greeting message.

Table of Contents

1. [Environment Setup](#environment-setup)  
2. [Install Foundry](#install-foundry)  
3. [Initialize Project](#initialize-project)  
4. [Create Smart Contract](#create-smart-contract)  
5. [Compile Contract](#compile-contract)  
6. [Create Wallet](#create-wallet)  
7. [Fund Wallet](#fund-wallet)  
8. [Deploy Contract](#deploy-contract)  
9. [Interact with Contract](#interact-with-contract)  
10. [What You’ve Achieved](#what-youve-achieved)  
11. [Troubleshooting & Notes](#troubleshooting--notes)  

## Environment Setup
Mac: Terminal
Windows: Ubuntu WSL (8GB RAM, 512GB storage)

Follow these steps to set up Ubuntu on Windows:

1. **System Requirements:** At least **8GB RAM** and **512GB storage**  
2. **Enable Features:**  
   - Search for *"Turn Windows features on or off"*  
   - Enable:
     - Virtual Machine Platform  
     - Windows Subsystem for Linux  
   - Restart your PC  
3. **Install Ubuntu:**  
   - Open Microsoft Store → Install **Ubuntu (no version number)**  
   - Launch and complete setup (username + password)  
4. **Fix Errors (if any):**  
   - Download kernel update: https://aka.ms/wsl2kernel  
   - Install and restart Ubuntu  

You can now use Ubuntu via the app or **VS Code WSL terminal**.


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

