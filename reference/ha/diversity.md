# Client Diversity

One risk that a node operator faces is a critical bug in a node. 
Even though some aspects of it could be mitigated via a good upgrade process (see ["Upgrading Nodes"](nodes/)),
but there are some issues or security vulnerabilities that could be uncovered
only when the issue is exploited in the real world.

Ethereum has multiple nodes, both CL and EL, that are produced by different
vendors, using different technologies (see also [Nodes](nodes/)). That helps
to avoid these risks, but only if there are no supermajority of any nodes that
will cause network to reach finality on a wrong chain.

For a staker, if it runs exclusively one type of nodes, it might cause
a problems of either 
* participation in the network being finalized on a wrong block;
* having all nodes disagreeing with the rest of the network, causing downtime
    or slashing (see also [Slashing And Penalties](slashing-and-penalties.md))

So, running diverse set of nodes is important for both health of Ethereum and
also for mitigating risk of the staker itself.

Use  [Client Diversity Dashboard](TODO: link?) to see which nodes to pick, and
make sure that you have a diverse enough set of nodes.


## Read More

* [Client Diversity Dashboard](https://clientdiversity.org)

* [EtherNodes: Execution Layer Stats](https://ethernodes.org)

* [NodeWatch: Consensus Layer Stats](https://www.nodewatch.io)
