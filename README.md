# Token Vesting Smart Contract

A robust and secure TokenVesting smart contract for managing time-locked tokens for beneficiaries like team members, advisors, or investors.

## Overview

This contract supports multiple, customizable vesting schedules, including linear and cliff-based releases. It's designed to hold ERC-20 tokens and release them to designated beneficiaries according to predefined schedules, ensuring tokens are distributed over a set period to align long-term incentives and prevent premature token dumps.

## Features

- **Multiple Beneficiaries**: Manage vesting schedules for any number of beneficiaries in a single contract
- **Customizable Schedules**: Each beneficiary can have a unique vesting schedule with specific start time, duration, and cliff period
- **ERC-20 Token Agnostic**: Can hold and vest any standard ERC-20 token
- **Linear Vesting**: Tokens are released proportionally over the vesting duration
- **Cliff Vesting**: A specified period at the beginning where no tokens are vested, followed by scheduled vesting
- **Irrevocable Schedules**: Once created, a vesting schedule cannot be modified
- **Claimable Tokens**: Beneficiaries can pull their vested tokens at any time
- **View Functions**: Check total vested amounts, releasable amounts, and schedule details
- **Ownership and Control**: Contract owner manages adding new vesting schedules

## Core Concepts

### Vesting Schedule

A vesting schedule is defined by these parameters:
- **Beneficiary**: Address that will receive the vested tokens
- **Start Timestamp**: When the vesting period begins
- **Duration**: Total length of the vesting period (in seconds)
- **Cliff Duration**: Initial period (in seconds) where no tokens are released
- **Total Amount**: Total number of tokens to be vested
- **Amount Released**: Number of tokens already claimed

### How Vesting is Calculated

The releasable tokens are calculated based on time elapsed since the vesting start:

- **Before Cliff**: No tokens can be released if current time is before start + cliff
- **After Cliff and During Vesting**: Vested amount is calculated linearly based on the proportion of vesting duration passed
- **After Vesting Period**: All remaining tokens are fully vested and can be released

## Usage

### Deployment

1. Deploy the TokenVesting contract with the address of the ERC-20 token it will manage
2. The deployer becomes the contract owner

### Token Transfer

Transfer the total amount of tokens to be vested to the deployed TokenVesting contract address. The contract needs to hold tokens to release them later.

### Create Vesting Schedule

The contract owner can:
- Call `createVestingSchedule` for each beneficiary with their vesting parameters
- Use `createMultipleVestingSchedules` to create schedules for multiple beneficiaries in a single transaction

### Beneficiary Claims Tokens

- Beneficiaries can call the `release` function to withdraw vested tokens at any time
- Check currently releasable amount using the `getReleasableAmount` view function

## Development

This project uses Hardhat for development, testing, and deployment. You'll need Node.js and npm/yarn installed.

## License

This project is licensed under the MIT License.