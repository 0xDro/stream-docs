---
sidebar_position: 1
slug: /
---

# Introduction to Stream Finance
Stream Finance provides vault structured protocols that help users take advantage of rate arbitrages, carry trades, and earn in the token of their choice. These strategies are actively managed for efficiency, and have historically out competed rivals. 

Here you can find in depth explanations of Stream’s products

## LevUSD Vaults - Earn in USD Terms

These vaults are dollar denominated and are meant to simply run the most efficient carry trade possible. Withdrawals and deposits are processed weekly on Fridays, and this process will happen across multiple chains. 

This style of vault works via two primary components; a derivative short and spot long. The short collects funding paid to shorters on a DEX such as DyDx, Hyperliquid, Aevo, etc. The vault then simultaneously goes long the same amount to cancel out exposure. This means that as long as these positions are managed, no matter how much the underlying asset (say ETH) goes up or down, the vault will be worth the same, as the short and long cancel each other out.

As a result, the vaults make money as a result of the difference between the cost to go long and how much the vault is paid to go short. As long as long cost < short payment, the vault will be profitable. During bull markets this has historically been the case. Cost to go long is roughly around 7-10% in USD terms. Funding rates can be checked on coinglass. As of writing the vault has been able to manage itself properly and has earned well over the projected 20% APY besides the first week. 

## HODL Vaults (DMM)- Earn in (ETH/BTC) 

HODL Vaults are similar to LevUSD vaults, in that they too take advantage of the difference between how much the vault can be paid to short and how much it costs to hedge out the short exposure. However, these vaults do not hedge out the underlying token. That can take the form of simply going long and short but hedging out the underlying position or it can take the form of borrowing against the token and then doing a delta neutral strategy. 

This allows users to earn in terms of their token of choice, while dollar denominated profits are used to DCA into the underlying asset and repeat the process. 

