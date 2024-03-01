
### What are instant withdrawals?
Instant withdrawals are a way to allow users to withdraw funds that were deposited in the same round. These are funds that have not yet been allocated to the strategy, and therefore when instantly withdrawing you can receive the exact amount of funds you deposited in the same round

### What is the process to withdraw funds?
The withdraw process is made up of 2 steps:
- Initiating a withdraw
- Completing a withdraw
  
This process is broken up into two steps to allow for asynchronous withdrawals

### What does it mean to initiate a withdraw?
Initiating a withdraw is the first step in receiving your funds from the vault. It signals to vault operators that you want to withdraw your funds. Before rolling to the next round, vault operators will withdraw the amount of initiated withdraws from the strategy and deposit it in the vault to be available for complete withdraw

:::note
If you have a previous outstanding withdraw that is available for completion, you won't be able to initiate a second withdraw until the first is completely withdrawn
:::

### What does it mean to complete a withdraw?
Completing a withdraw means receiving back your deposit + any yield accrued in the vault. You may only complete a withdraw in a round if you initiated a withdraw in a previous round. You will receive the underlying asset of the vault.

### When do you instantly withdraw and when do you initiate a withdraw?
You can instantly withdraw if withdrawing funds from the same round you deposited in. If a round has passed between the time of depositing and when you want to withdraw, you must initiate a withdraw

### How can I self-custody my vault shares?
It is possible to self-custody your vault shares through the `redeem(uint256 numShares)` function





