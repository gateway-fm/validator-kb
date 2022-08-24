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
a [separate chapter](validator-clients.md) about them, since the topic is very important.

## Nodes Health

To serve as a validator, both CL and EL needs to be up to date with the
network. There are a couple of techniques of how to check that.

All this healthchecks data should lead to a [monitoring tool](monitoring.md) of your choice.

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
system](monitoring.md).

### Source Of Truth Checks (Forks)

Finally, the case when the blocks are being synced, but you are on the wrong
fork. Detection of that could happen on the EL very easily, by using the block
hash of returned from [`eth_getBlockByNumber("latest", false)`](https://docs.gateway.fm/v/api-docs/ethereum/eth_getblockbynumber).

You can compare these hashes across the nodes and also across the external
sources of truth.

## Provisioning Nodes

Provisioning nodes quickly is very important both for scalability and for
disaster recovery reasons. You don't want to wait a couple of days until your
nodes are ready to be validated.

There are ways of how to quickly provision nodes on both layers.

### Provisining Execution Layer

Execution layer node is the heavier one of the two. There is no universal way
of quickly provisioning the node. The usual way is to copy some files from a datadir.

It is important not to copy the full datadir because that could lead to multiple
nodes having the same peer ID and having troubles connecting to the same peers.
Eth1 p2p protocol devp2p forbids connecting multiple nodes with the same ID to
the same peer. Only the first one will be connected, the rest will be dropped.

Files to copy:
* Besu - <TBD>
* Erigon - `<datadir>/chaindata` && `<datadir>/snapshots`.
* Geth - <TBD>
* Nethermind - `<datadir>/db`

### Provisioning Consensus Layer

First, it is important to note that provisioning consensus layer via snapshots
of data folder is a bad practice. Multiple nodes might end up with the same
node ID, and that will bring issues during peers discovery (only one node with
a certain ID could be connected to the peers).

Good news, is that all CL nodes have a cross-compatbile way of syncing quickly:
**checkpoint sync**. What it does, is it takes the latest blockchain state from
another node (or a file) and applies it w/o doing all the necessary checks.
**Only use trusted source nodes for Checkpoint sync!**.

* Lighthouse: https://lighthouse-book.sigmaprime.io/checkpoint-sync.html
* Lodestar: (use `--checkpointSyncUrl`, see https://chainsafe.github.io/lodestar/reference/cli/)
* Nimbus: https://nimbus.guide/trusted-node-sync.html
* Prysm: https://docs.prylabs.network/docs/prysm-usage/checkpoint-sync
* Teku: https://docs.teku.consensys.net/en/latest/HowTo/Get-Started/Checkpoint-Start/

**Checkpoint Sync From A File**

For most of the CL nodes, you can store the latest state of the network into
a file, in SSZ format and use that instead of another node. That is useful if
you don't have any trusted node or you have to re-created the setup after it
being completely lost.

A good practice is to keep this file upgraded once every week.

## Upgrading Nodes


## Security, Networking & Sentries

## Hardware Specs & Cloud Machines

## Troubleshooting
