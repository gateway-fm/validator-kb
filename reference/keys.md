# Key Management

## Types Of Keys

In staking, there are up to 4 types of keys involved. In theory they all could be independent, but in practice you can reuse the same keys for **Deposit Keys**, **Withdrawal Keys** and **Fee Recipient Keys**.

**Signing Keys** should be separate because these are the only keys that must be always available on the validator nodes, they they are the most risky ones.

### Deposit Keys

**Depositor Keys** - the keys that are used to sing a deposit transactions, basically the keys to a wallet with 32 eth.

### Signing Keys

**Signing Keys** — the keys that validator client uses to sign blocks when it produces it.

They are also used to exit the set of validators.

### Withdrawal Keys

**Withdrawal Keys** - the keys to an account that allow to withdraw money after the validator was exited, and potentially allowing re-staking.

### Fee Recipient Keys

These are the keys to an account where the transaction fees are being collected.

## Key Management

### 3rd party custody

## CoinCover

## Copper

## Balance
