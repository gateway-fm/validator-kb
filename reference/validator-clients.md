# Validator Clients

The validator client is the software that runs on top of a beacon node and
attests to the exising chain as well as produces blocks. It is similar to
a mining software for the old POW version of ETH.

Validator client != validator. Validator is a pair of (pubk, pk) that is used
to sign attestations and blocks. 

Each validator client could handle multiple validators. 
How many? There is no universal answer, but for eth mainnet,
most organiations put 100 or 200 validators per a single validator
client.

## Built-in Validator Clients

Each [beacon node](nodes.md) team has a validator client.

* [Prysm](https://docs.prylabs.network/docs/how-prysm-works/prysm-validator-client)
* [Lighthouse](https://lighthouse-book.sigmaprime.io/mainnet-validator.html#docker-users)
* Nimbus
* Teku

Since the separate validator clients are using [standard APIs](https://ethereum.github.io/beacon-APIs/), you don't have to match them with the beacon nodes. For example, Lighthouse's
validator client can easily be used with Prysm, etc.

## External Validator Clients

### [Vouch](https://github.com/attestantio/vouch) 

Vouch is a multi-node highly-available validator client, developed by
Attestant. It allows to use multiple nodes at once to make sure that your
system is always as available and as efficient as possible.

It has a relatively steep learning curve, but it is very flexible in its
configuration.

## External Signer / Wallet

The biggest risk of running a validator client is keys being lost or stolen. To
improve security over that, it is advised to not keep the keys on the
nodes/validator clients, but instead use a separate client, so called "externa"
or "remote" signer. That allows for better separation of responsibilities, and
for smaller attach surface, because only the machine with the keys needs most
protection.

### [Dirk](https://github.com/attestantio/dirk)

Supported by Vouch. Dirk is a very comprehensive external signer, with
[extensive system of permissions](https://github.com/attestantio/dirk/blob/master/docs/permissions.md)
and using TLS for both authentication and encryption.

It also supports [distributed key generation and signing](https://github.com/attestantio/dirk/blob/master/docs/distributed_key_generation.md),  making the system more highly available and secure.

The biggest downside is that it has a steep learning curve and also it supports
only Vouch as a validator client.

* [Getting Started With
    Dirk](https://github.com/attestantio/dirk/blob/master/docs/getting_started.md)


### [Web3 Signer](https://docs.web3signer.consensys.net/en/latest/)

Supported [Teku](https://docs.teku.consensys.net/en/latest/HowTo/External-Signer/Use-External-Signer/), 
[Prysm](https://docs.prylabs.network/docs/wallet/web3signer) and
[Lighthouse](https://lighthouse-book.sigmaprime.io/validator-web3signer.html)

## SSV

TBD

## Validator Performance Metrics

### Participation Rate

TBD

### Block Proposal

TBD

## Validator Client Diversity

To reduce the risk of being exposed to a bug or technological decision 
in one validator client, it is a good practice run different validator clients.

Even though the validator clients use the same API, there is no standard of
storing keys in them.

There are two options on how it is possible to run them:

**Diversify online validator clients**: run different validator clients at the
same time, for different validators. For example, run Vouch for validators 0 to
99, run Lighthouse for validators 100 to 199, etc. Upside: the whole system is
resilient toward issues in a signle validator clients, not all of them will go
down at the same time. Downside: adds complications to the setup, monitoring
and managing validator clients.

**Diversify cold backup**: run the same validator clients across all
validators, and keep keystores and launch scripts ready for another validator
client to replace it in case of disaster. Upside of this approach: easy to
manage online validator clients, simple setup. Downside: in case of an issue in
a validator client, all validators will be offline at the same time.


## Validator Clients Redundancy

Validator clients like Lighthouse and Vouch support HA redundancy. They can
look at multiple beacon nodes at the same time to use for block proposals and
attestation. That increases chances of validator being available even if one of
the nodes is unavailable.

## Slashings & Slashing DB

To prevent being slahed, each validator client keeps a slashing DB that has
slasheable blocks to avoid attesting.

see also [Slashing And Penalties](slashings-and-penalties.md)


## Further Reading

* [Eth 2.0 Annotated Spec: Validator Duties, Rewards & Penalties](https://github.com/ethereum/annotated-spec/blob/master/altair/beacon-chain.md#aside-validator-duties-rewards-and-penalties)

* [Eth 2.0 Annotated Spec](https://benjaminion.xyz/eth2-annotated-spec/)
