# High Availability

## Redundancy For Validators

In web2 world, whenever one wants to make things highly available, they usualy run a redundant setup.

**Redundancy**

For example, you run copies of a database across multiple servers and use them
at the same time, removing single points of failure. In this case, you use
multiple copies of a service at the same time.

**Failover**

That happens, when one region or one copy of the environment goes down, all the
traffic gets automatically redistributed to another copy. The difference
between failover and redundant setup is subtle but could be said as, "in
redundant setup, multiple copies are used during normal functioning of the
system; in the failover setup copies are only used when the main one goes
down."

Failover can happen automatically, or manually.

**Validators**

So, to validate, you need 4 components.

* Consensus Layer Node (beacon node)
* Execution Layer Node
* Validator Client
* Wallet

Nodes are generally heavy. Validator client is almost stateless, and the wallet
only contains block signing keys.

If we take [Slashing and Penalties](slashing-and-penalties.md) into account, we
can come to a following setup.

* Consensus Layer + Executuion Layers -- use redundancy. Many validator
    clients (Vouch, Lighthouse, see [Validator Clients](validator-clients.md))
    allow to follow multiple nodes at the same time.

* [Validator Client](validator-client.md) + Wallet -- use manual failover. Inactivity leaks are
    usually not the end of the world, but running multiple validator clients
    with the same set of keys even by mistake could lead to a slashable offence
    and losing one of more validators (see more [Slashing and Penalties](slashing-and-penalties.md).

* Use independent [monitoring](monitoring.md) to see if your validators are
    actually down and not responding.

That way, you have a single point of failure at [validator
clients](validator-clients.md), but if you know about it and [monitor it properly](monitoring.md), 
it won't cause a big risk.

### Distributed Validator Clients

**SSV**

## Geographical Distribution

## Client Diversity

One risk that a node operator faces is a critical bug in a node. 
Even though some aspects of it could be mitigated via a good upgrade process (see ["Upgrading Nodes"](nodes.md)),
but there are some issues or security vulnerabilities that could be uncovered
only when the issue is exploited in the real world.

Ethereum has multiple nodes, both CL and EL, that are produced by different
vendors, using different technologies (see also [Nodes](nodes.md)). That helps
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

## Further Reading

* [Slashing & Penalties](slashing-and-penalties.md)

* [Client Diversity Dashboard](https://clientdiversity.org)

* [EtherNodes: Execution Layer Stats](https://ethernodes.org)

* [NodeWatch: Consensus Layer Stats](https://www.nodewatch.io)


## BACKLOG
    - Resources scaling
        - CPU, RAM
        - Disks

## Resource Scaling
Extra space to allocate in terms of non-finality / Or being able to extend the filesystem quickly
Info on archive node and what it means in CL context
When/How to scale up the setup? What to look out for while scaling?
