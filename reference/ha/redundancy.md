# Redundancy & Failover

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

## Read More

* [Slashing & Penalties](slashing-and-penalties.md)

