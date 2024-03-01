
### What are instant withdrawals?
Instant withdrawals allow users to withdraw funds that were deposited in the same round. These are funds that have not yet been allocated to the strategy. Therefore, when instantly withdrawing, you can receive the exact amount of funds you deposited in the same round.

### What is the process to withdraw funds?
The withdraw process is made up of 2 steps:
- Initiating a withdraw
- Completing a withdraw
  
This process is broken up into two steps to allow for asynchronous withdrawals

### What does it mean to initiate a withdraw?
Initiating a withdrawal is the first step in receiving your funds from the vault. It signals to vault operators that you want to withdraw your funds. Before rolling over to the next round, vault operators will withdraw the amount of initiated withdrawals from the strategy and deposit it in the vault to be available for complete withdrawal.

:::note
If you have a previous outstanding withdrawal that is available for completion, you won't be able to initiate a second withdrawal until the first is completely withdrawn.
:::

### What does it mean to complete a withdraw?
Completing a withdrawal means receiving back your deposit + any yield accrued in the vault. You may only complete a withdrawal in a round if you initiated a withdrawal in a previous round. You will receive the underlying asset of the vault.

### When do you instantly withdraw and when do you initiate a withdraw?
You can instantly withdraw if withdrawing funds from the same round you deposited in. If a round has passed between the time of depositing and when you want to withdraw, you must initiate a withdrawal.

### How can I self-custody my vault shares?
You can self-custody your vault shares through the `redeem(uint256 numShares)` function.





