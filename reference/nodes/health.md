# Nodes Health

How can you know a node is healthy? Most importantly how can you check it programatically? It is one of the criterias to monitor validator service at scale. 

## Basic health check from the node
Most of the node clients have implemented the healthcheck API endpoint. For example, Lighthouse has an endpoint called "/lighthouse/health". It should return "HTTP 200 OK" when everything is setup correctly, all other responses mean the node software is having issue.

It is usually the most basic check and only tells you that software is up and running. So one shouldn't rely on it solely.

## Different health symptoms

Here are a few common symtoms and their causes.


Some of the following symtoms are urgent, which means it has been fixed immediately. Some will only show that the system is degrading but it will 
It's important to be able to check a node health
How to check if a node is healthy
To serve as a validator, both CL and EL need to be up to date with the
network. There are a couple of techniques of how to check that.

All this healthchecks data should lead to a [monitoring tool](../ha/monitoring.md) of your choice.

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
