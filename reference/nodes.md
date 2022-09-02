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
To check the ID of your node use `admin_nodeInfo` RPC call, `enode` field.

Files to copy:
* Besu - <TBD>
* Erigon - `<datadir>/chaindata` && `<datadir>/snapshots` (also need to copy `<datadir>/clique if you have it).
* Geth - `<datadir>`
* Nethermind - `<datadir>/db`

### Provisioning Consensus Layer (Checkpoint Sync)

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

**Public Checkpoint Sync Endpoints**

Usually, you should strive to use your own nodes as source of data for checkpoint sync, but if you can’t, there are a couple of public places where you can sync from:

* Open Endpoints
    * Ethereum Foundation
        * Goerli: https://goerli.checkpoint-sync.ethdevops.io
        * Sepolia: https://sepolia.checkpoint-sync.ethdevops.io
        * Mainnet: TBD
    * gateway.fm (link TBD)
    * nethermind (link TB

* Registration Needed
    * Infura: infura.io; beacon API.

When syncing from one of the public sources, always validate that your node is synced to the correct chain. Use [this article](https://notes.ethereum.org/@launchpad/checkpoint-sync#Step-4) to learn how to do that.

In Prysm you can also use `—-weak-subjectivity-checkpoint` flag (read more [here](https://docs.prylabs.network/docs/prysm-usage/parameters)).


**Checkpoint Sync From A File**

For most of the CL nodes, you can store the latest state of the network into
a file, in SSZ format and use that instead of another node. That is useful if
you don't have any trusted node or you have to re-created the setup after it
being completely lost.

Most of the nodes require both the latest finalized state and the block corresponding to the finalized state.

A good practice is to keep these files upgraded once every week.

How to create these files, you can read here: [“Sync from checkpoint files” in Nimbus Guide](https://nimbus.guide/trusted-node-sync.html#sync-from-checkpoint-files). The files obtained there are cross-node compatible.

## Upgrading Nodes

Upgrading nodes in time is important for two reasons.

Firstly, there are security issues that are fixed in the nodes all the time.

Secondly, it is important to keep track of the hardforks. If hardfork comes and your node is not upgraded, it will use the wrong chain fork.

**Being informed of node upgrades and hardforks**

Most of the nodes are on GitHub. There is [a feature to notify of new releases](https://docs.github.com/en/account-and-profile/managing-subscriptions-and-notifications-on-github/managing-subscriptions-for-activity-on-github/viewing-your-subscriptions). Also you can use this [Slack bot](https://github.com/nightskylark/github-releases-slack-notifier) that notifies about new releases of software.

There are the official channels to follow on Twitter, to be aware of new releases, bugs and features.

Execution layer: 

* Geth: 
    * Twitter: https://twitter.com/go_ethereum

* Erigon: 
    * Twitter: https://twitter.com/erigoneth
    * Newsletter: https://erigon.substack.com

* Nethermind: 
    * Twitter: https://twitter.com/nethermindeth
    * Blog: https://medium.com/nethermind-eth

Consensus layer:

* Prysm
    * Twitter: https://twitter.com/prylabs

* Lighthouse
    * Twitter: https://twitter.com/sigp_io

* Lodestar
    * Twitter: https://twitter.com/lodestar_eth

* Teku:
    * Twitter: https://twitter.com/Teku_ConsenSys

* Nimbus: 
    * Twitter: https://twitter.com/ethnimbus
    * Newsletter: https://subscribe.nimbus.guide/ 

Validator clients:

* Dirk

* Vouch


Other channels of information about upcoming changes to the network:

* Ethstaker

* Ethereum Foundation twitter and blog


**Canary Nodes** 

Since new releases of nodes can contain bugs, and often critical ones, it is important not to upgrade all nodes at once. 

Good practice is to have “canary” nodes that are upgraded first and monitored for a couple of days (important to get the node through at least one restart through the process, in the past there were cases when the data corruption was only visible after restarts).

If canary nodes show no regressions after 3-7 days, all nodes are upgraded to the new release.

Always keep at least one backup of the node data from the previous build to be able to downgrade! Sometimes nodes update the format of embedded database and after migration it is impossible to go back.

## Security, Networking & Sentries

## Hardware Specs & Cloud Machines

## Troubleshooting
