# Nodes

To run nodes, you need 

Consensus Layer (CL) node, one of

* Lighthouse
* Lodestar
* Nimbus
* Prysm
* Teku

Execution Layer (EL) node, one of

* Besu
* Erigon
* Geth
* Nethermind

This chapter doesn't include the information about validator clients, there is
a [separate chapter](reference/validator-clients.md) about them, since the topic is very important.

## Nodes Health

To serve as a validator, both CL and EL needs to be up to date with the
network. There are a couple of techniques of how to check that.

All this healthchecks data should lead to a [monitoring tool](reference/monitoring.md) of your choice.

### Internal healthchecks

Most of the nodes have exposed healthchecks APIs, that return `HTTP 5xx` if the node
is not syncing properly, and `HTTP 200 OK` if everything is okay. That is the most simple
and most basic version of the healthcheck.

### Timestamp Checks

One more strategy is based on the timestamp of the latest block.

For EL that is a response to [`eth_getBlockByNumber("latest", false)`](https://docs.gateway.fm/v/api-docs/ethereum/eth_getblockbynumber).

It has a field called `timestamp`. By knowing the timestamp of the block and the block production rate (1 block per 12 seconds), it is
possible to see how "old" is the current block of the node.

Since sometimes the block proposals could be missed, it doesn't make sense to
keep this threshold too tight, but if it is > 5 minutes old, it makes sense to
mark the node as "unhealthy" and notify your [monitoring
system](reference/monitoring.md).

### Source Of Truth Checks (Forks)

Finally, the case when the blocks are being synced, but you are on the wrong
fork. Detection of that could happen on the EL very easily, by using the block
hash of returned from [`eth_getBlockByNumber("latest", false)`](https://docs.gateway.fm/v/api-docs/ethereum/eth_getblockbynumber).

You can compare these hashes across the nodes and also across the external
sources of truth.

## Provisioning Nodes

### Provisioning Consensus Layer

* Checkpoint Sync

### Provisining Execution Layer

Snapshots of the database

## Upgrading Nodes


## Security, Networking & Sentries

## Hardware Specs & Cloud Machines
