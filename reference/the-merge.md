# The Merge

The merge is the process of switching Ethereum from Proof-Of-Work to
Proof-Of-Stake consensus mechanism.

It is called like that because it merges the existing beacon chain (previously
called eth 2.0) with the mainnet.

It is technically achieved through a special protocol between two nodes, one
beacon node (called **Consensus Layer**) and one eth1 node (called **Execution
Layer**) and moving responsibilities for consensus, block production, fork
choice rules to the Consensus Layer.

On the other hand, Consensus Layer cannot by itself, perform block proposals and even attesting to the blocks.
It uses Execution Layer to check the block validity as well as execute
transactions and propose new block contents.

For a staker it means that instead of one node, you need to run two nodes
side-by-side, one Consensus Layer, one Execution Layer.

You need to run them in one-to-one relationship. Running multiple Consensus Layers per one Execution Layer is forbidden by the
specification (TODO: link). Running multiple Execution Layers per a Consensus
Layer is technically not forbidden, but this configuration is untested and not
recommended.

See also:
* [Nodes](nodes/)
