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

* Prysm
* Lighthouse
* Nimbus
* Teku

Since the separate validator clients are using a standard API [LINK??], you
don't have to match them with the beacon nodes. For example, Lighthouse's
validator client can easily be used with Prysm, etc.

## External Validator Clients

* Vouch

## SSV

TBD

## Validator Performance Metrics

(see also [eth2 specs with comments](link???))

### Participation Rate

### Block Proposal

## Validator Client Diversity

To reduce the risk of being exposed to a bug in one validator client, it is
a good practice run different validator clients.

There are two options on how it is possible to run them:

* diversify via running them at the same time

* diversify for backup purposes


## Validator Clients Redundancy

Validator clients like Lighthouse and Vouch support HA redundancy. They can
look at multiple beacon nodes at the same time to use for block proposals and
attestation. That increases chances of validator being available even if one of
the nodes is unavailable.

