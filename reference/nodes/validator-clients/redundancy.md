# Validator Clients Redundancy

Validator clients like Lighthouse and Vouch support HA redundancy. They can
look at multiple beacon nodes at the same time to use for block proposals and
attestation. That increases chances of validator being available even if one of
the nodes is unavailable.

## Slashings & Slashing DB

To prevent being slashed, each validator client keeps a slashing DB that has
slasheable blocks to avoid attesting.

## Read More

* [Slashing And Penalties](../basics/slashings-and-penalties.md)

* [Eth 2.0 Annotated Spec: Validator Duties, Rewards & Penalties](https://github.com/ethereum/annotated-spec/blob/master/altair/beacon-chain.md#aside-validator-duties-rewards-and-penalties)

* [Eth 2.0 Annotated Spec](https://benjaminion.xyz/eth2-annotated-spec/)

