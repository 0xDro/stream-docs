## Overview

Stream vaults are vaults composed as a solidity contract that follow a round-by-round model. Every week, the vault round gets rolled over by a specialized role called the vault keeper. Ownership over the vault is represented by an underlying ERC20 as "shares". Each vault has a specific underlying ERC20 which represents the token that deposits are accepted in. Additionally, the vaults allow for asynchronous withdraw through an initiate-confirm withdraw process. Finally the vaults also allow for self-custody of share tokens rather than sitting in the smart contract enabling composability of vault ownership represenatationship.


## Vault Deposit Flow

![Vault Deposit Flow Diagram](/img/StreamFlow.png)

1. User deposits 1000 USDC into LevUSDC Vault in round n through `deposit()` or `depositFor()`
2. The contract creates an entry in `depositReceipt.amount` for 1000 USDC and updates `vaultState.totalPending`
3. Vault Keeper rolls the contract through `rollToNextRound()` to advance the round to n+1 
4. Upon rolling the 1000 USDC is transfered to the Vault Keeper and corresponding shares are minted
5. The 1000 USDC is utilized in the active DMM strategy

## Vault Withdraw Flow

Stream Vaults allow for two types of withdraws: asynchronous withdraws and same-round-withdraws (instant withdraws)

![Vault Instant Withdraw Flow Diagram](/img/WithdrawInstantFlow.png)
### Instant Withdraws
Instant withdraws are only available when a user withdraws tokens in the same round they were deposited. These withdraws are fulfilled instantly as their tokens have not yet been deposited in the DMM strategy, but rather are still in a pending state in the smart contracts.

1. User deposits 1000 USDC into LevUSDC Vault in round n through `deposit()` or `depositFor()`
2. The contract creates an entry in `depositReceipt.amount` for 1000 USDC
3. User changes their mind on size and withdraws 500 USDC through `instantWithdraw()`
4. User receives 500 USDC and updates `depositReceipt.amount` to be the remaining 500 USDC

![Vault Async Withdraw Flow Diagram](/img/AsyncWithdrawFlow.png)

### Asynchronous Withdraws
Asynchronous withdraws occur when a user deposited in a previous round, has their funds operating in the DMM strategy, and now want to make a request to withdraw their funds. In this scenario a request is made and only fulfilled at the time of the next round rollover. This means a user can wait -- in the worst case -- a week long to receive their deposited funds + yield through a secondary call to the vault's contracts after the rollover.

1. User deposits 1000 USDC into LevUSDC Vault in round n through `deposit()` or `depositFor()`
2. The contract creates an entry in `depositReceipt.amount` for 1000 USDC
3. Vault Keeper rolls the contract through `rollToNextRound()` to advance the round to n+1
4. Upon rolling the 1000 USDC is transfered to the Vault Keeper
5. The 1000 USDC is utilized in the active DMM strategy
6. User decides to withdraw funds and creates a call to `initiateWithdraw()` for 1000 USDC in round n+1
7. A `withdrawReceipt` is created for the amount of shares 1000 USDC in round n accounts for -- say 10 shares -- while updating `currentQueuedWithdrawShares` accordingly
8. Vault Keeper rolls over round to n+2 and deposits (1000 + captured yield) USDC to fulfill 10 shares (calculated when rolling over round)
9. In round n+2 the user makes a call to `completeWithdraw()` and the contract sends 1000 USDC + yield to the user
10. `currentQueuedWithdrawShares` and `withdrawReceipt` is updated to maintain proper state while burned 10 shares

### Redemption Flow
After a user deposit is processed and utilized in the DMM strategy, the user has the ability to either have the vault custody their shares or withdraw/hold their shares themselves.


1. User deposits 1000 USDC into LevUSDC Vault in round n through `deposit()` or `depositFor()`
2. The contract creates an entry in `depositReceipt.amount` for 1000 USDC
3. Vault Keeper rolls the contract through `rollToNextRound()` to advance the round to n+1
4. Upon rolling the 1000 USDC is transfered to the Vault Keeper
5. The 1000 USDC is utilized in the active DMM strategy
6. User wants to hold their shares and call `redeem()` or `maxRedeem()`
7. User receives vault shares ERC20 and `depositReceipt.amount` is set to 0 while setting `depositReceipt.unredeemedShares` to the amount of shares withdrawn

:::note
When a user decides to withdraw funds after holding their own shares, they don't need to approve the vault token to send shares to the vault in order to be burned. The vault and only the vault can transfer without traditional approval permission
:::
