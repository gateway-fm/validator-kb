# Full vs. Archival Nodes

Ethereum had a notion of an archival node, the node that keeps all **state data** from the beginning of the chain, and allows for some cool properties, like retracing transactions from the past, or seeing the exact state of the Ethereum at any block. If you want to run an archival node, Erigon is the best choice at the moment.

There are also full nodes. Full nodes _validate all the blockchain_ and also serve blocks and headers for other nodes to catch up with the sync. Full node don’t keep all state changes from the beginning of the chain, they keep enough to allow for forks to be resolved. They take much less disk space.

Full nodes still validate the full blockchain.

You don’t need archival nodes to run a Validator, a full node is enough.

After [The Merge](the-merge.md), archival nodes usually means doing archival for the EL to keep all smart contract state data, and keep the Consensus node as a Full node.

But sometimes you also might be interested in running CL in archival mode, that allows for tracing all historical changes in the list of Validators, getting statistics and analytics from the beginning of the chain.
