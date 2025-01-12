# Unhandled Exception in Ownership Transfer

This repository demonstrates a common vulnerability in smart contracts related to ownership transfer. The bug involves a missing check for the caller's authority before transferring ownership.  An attacker could exploit this by sending a transaction that would normally fail, but instead of a clear rejection, it remains in a failed state, preventing any subsequent actions by the owner.

## Vulnerability
The `transferOwnership` function lacks a check to ensure that only the current owner can initiate the ownership transfer.  This allows any address to call `transferOwnership` and potentially block the ownership transfer by passing a valid but malicious `newOwner` address that causes an unexpected error.

## Solution
The solution includes adding a `require(msg.sender == owner, "Ownable: caller is not the owner");` check at the beginning of the `transferOwnership` function. This ensures only the current owner can transfer ownership.