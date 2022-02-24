---
description: Abbreviated as ED
---

# Existential Deposit

Accounts in ICE blockchain should have a certain minimum balance (Existential Deposit) so that the account can exist on-chain. This helps prevent bloating of the chain state.

For Frost Network, the value of Existential Deposit is fixed at **500 Atto** (_subject to change later_).

If the balance of a wallet goes below the ED, the account will be reaped i.e. the account information will be cleared from the blockchain. The account nonce will be reset and all the tokens held by the wallet will be wiped. However the user holding the account’s private key still has access to the wallet.

More info [here](https://support.polkadot.network/support/solutions/articles/65000168651-what-is-the-existential-deposit-#:\~:text=This%20minimum%20amount%20is%20called,performance%20and%20to%20reduce%20fees.)
