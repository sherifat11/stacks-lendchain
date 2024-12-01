# Decentralized Lending and Microfinance Smart Contract

## Overview

The Decentralized Lending and Microfinance Smart Contract is a blockchain-based solution built on the Stacks protocol. It facilitates a secure, transparent, and efficient lending system, enabling lenders to provide liquidity and borrowers to access loans without intermediaries. The contract includes robust state management and error handling to ensure safe and predictable operations.

---

## Features

### Lender Capabilities
- **Fund Lending Pool**: Lenders can deposit STX tokens into the lending pool to support loans.
- **Track Contributions**: Lenders can view their pool share and last contribution block.

### Borrower Capabilities
- **Request Loans**: Borrowers can apply for loans specifying the amount and term.
- **Repay Loans**: Borrowers can make repayments in installments or fully settle the loan.
- **View Loan Details**: Borrowers can access the current status and history of their loans.

### Administrative Capabilities
- **Contract Management**: The contract owner can pause and resume operations as needed.
- **Update Loan Records**: The administrator can manually update loan statuses for exceptional cases.

---

## Contract Structure

### Constants
- **Error Codes**: Defined for common issues like invalid inputs, insufficient balance, or unauthorized access (e.g., `ERR-INSUFFICIENT-BALANCE`, `ERR-LOAN-EXISTS`).
- **Loan Limits**: Minimum and maximum limits for loan amounts, durations, and interest rates.
- **Blockchain Assumptions**: Constants for estimating time-related parameters (e.g., blocks per day).

### Data Variables
- **Contract State**: Indicates whether the contract is active or paused.
- **Pool Metrics**: Tracks the total funds available in the pool and the number of active loans.

### Data Maps
- **Loan Records**: Stores details of loans, including principal, interest rate, term, repayment status, and borrower reputation.
- **Lender Contributions**: Tracks the amount and timing of each lender’s contributions.

---

## Core Functionalities

### Public Functions

#### 1. **Fund Lending Pool**
- **Parameters**:
  - `amount (uint)`: The amount of STX to contribute to the pool.
- **Description**: Adds funds to the lending pool and updates the lender's share.
- **Error Handling**:
  - Rejects contributions if the contract is paused or the amount is invalid.

#### 2. **Request Loan**
- **Parameters**:
  - `amount (uint)`: Requested loan amount.
  - `term-blocks (uint)`: Loan term in blocks.
- **Description**: Allows borrowers to request loans by transferring funds from the pool.
- **Error Handling**:
  - Validates the loan amount, term, and pool balance.
  - Ensures no existing active loans for the borrower.

#### 3. **Repay Loan**
- **Parameters**:
  - `amount (uint)`: Repayment amount.
- **Description**: Processes repayments from borrowers, updates loan status, and returns funds to the pool.
- **Error Handling**:
  - Rejects if the repayment amount is invalid or the loan has expired.

#### 4. **Pause/Resume Contract**
- **Parameters**: None.
- **Description**: Temporarily halts or resumes contract operations.

#### 5. **Update Loan Status**
- **Parameters**:
  - `borrower (principal)`: Borrower's address.
  - `new-status (string-ascii 20)`: New loan status.
- **Description**: Updates the loan status, such as marking it as "COMPLETED" or "DEFAULTED."

### Read-Only Functions

#### 1. **Calculate Interest**
- **Parameters**:
  - `principal (uint)`: Loan amount.
  - `rate (uint)`: Annual interest rate (as a fraction of 1,000,000).
- **Description**: Computes the total interest for a given principal and rate.

#### 2. **View Loan Details**
- **Parameters**:
  - `borrower (principal)`: Address of the borrower.
- **Description**: Retrieves the details of a borrower's loan.

#### 3. **View Pool Share**
- **Parameters**:
  - `lender (principal)`: Address of the lender.
- **Description**: Displays the lender's contribution and last deposit block.

#### 4. **View Pool Metrics**
- **Parameters**: None.
- **Description**: Returns the total funds in the pool.

---

## Deployment Instructions

1. **Environment Setup**:
   - Install Clarity development tools.
   - Prepare a Stacks wallet for contract deployment.

2. **Deploy Contract**:
   - Use the Stacks CLI or Clarinet to deploy the contract.
   - Ensure the deployer's address is set as the `contract-owner`.

3. **Initialize Pool**:
   - Lenders should contribute funds to activate borrowing functionality.

---

## Testing

### Unit Testing
- Validate error scenarios such as invalid loan requests or over-contributions.
- Test all edge cases for repayment calculations and pool updates.

### Integration Testing
- Simulate real-world scenarios involving multiple lenders and borrowers.
- Test for accurate state transitions, including loan completions and defaults.

---

## Security Considerations
- **Input Validation**: Ensures all inputs are within defined limits.
- **Overflow/Underflow Protection**: Implements safe arithmetic operations.
- **Emergency Controls**: Allows the contract owner to halt operations during emergencies.
- **Borrower Reputation**: Tracks borrower reliability for future creditworthiness.

---
