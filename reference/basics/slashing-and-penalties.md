# Slashing & Penalties

## Slashing

If your validator is slashed, it exits the set of active validators
immediately. Until withdrawals are activated, that means that the stake that
was used is locked and is unusable.

The validator can not be re-enabled after it was slashed.

Luckily, there are only three slasheable offences in the beacon chain
validation.

* Being a block proposer, and proposing 2 different blocks for the same slot
* Being an attester and signing two different attestations with the same target slot (attesting for two different blocks for the same slot, “double voting”)
* Being an attester and voting against history.

Most often, slashing happens when > 1 Validator client shares the same key set.

To avoid that, but still set up the redundancy, see the following chapters:

* [High Availability](ha.md)

* [Validator Clients](validator-clients.md)


## Inactivity Penalties

For other penalties, your validator could lose the stake but it won't be
removed from the set of validators while it balance is > 16 ETH.

If it goes all the way to 16 ETH, it will be ejected from the set and it will
not be able to re-join again.

The inactivity penalties include:

* Not attesting to the blockchain head block

* Not proposing a block when its time to do so

* Proposing invalid blocks

To prevent inactivity penalties, setup monitoring and alerting properly and
keep your nodes up to date. You can read more in the following chapters:

* [Monitoring And Alerting](monitoring.md)

* [Keep node up-to-date](reference/nodes/updates-releases.md)

## Further Reading

* [Rewards & Penalties on Eth2.0](https://consensys.net/blog/codefi/rewards-and-penalties-on-ethereum-20-phase-0/)

* [Eth 2.0 Annotated Spec: Validator Duties, Rewards & Penalties](https://github.com/ethereum/annotated-spec/blob/master/altair/beacon-chain.md#aside-validator-duties-rewards-and-penalties)
