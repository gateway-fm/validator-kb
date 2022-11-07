# Resource Scaling


## Resource usage

Node resource usage.

## Validators



## Disks & Storage

It is advised to use SSD disks for validators. NVMe are more expensive and unless you want to push the node to its limits, they make very little difference.

Free disk space should be monitored at all times (see [Monitoring](monitoring.md) for more info). Nodes use embedded databases that grow even when they prune unnecessary data, due to DB fragmentation, etc.

Make sure that you have about 20% free disk space at all times.

Every once in a while you might need to expand the disk. Many cloud solutions offer expanding data disk.

One important thing for expanding data disks for all nodes, is make sure that the node shutdown was clean (doesn’t matter if that Consensus or Execution layer).

That means sending the shutdown signal to the node and waiting for it to stop and flush all data to the disk. Most of the nodes (Erigon is notable exception) use a non-transactional DBs to store data and this data could get easily corrupted.


## Network

Having a good network of peers makes sure that your node’s participation rate is high, on all parameters. HEAD (voting on the chain head) is especially sensitive to the network.

Ideally you want a symmetric network with good throughout (100mb/s+) with proper external IP access, so you can handle 100-200 peers per node. The more peers you have, the higher will be traffic, but the more chances will be that your attestations will be included in time, and ultimately, that leads to more rewards.

## CPU

Both [Nodes](nodes/) and [validator clients](validator-clients.md) require significant CPU resources. Nodes needs to be able to sync, verify consensus, build blocks (unless you use [MEV-Boost](mev.md) and propagate validator duties into the network. Validator clients need to be generating signatures, signing block payloads for, usually, multiple validators at a time.

It is not recommended to go below 16Ghz for every piece of the setup: CL, EL, Validator Client.


## Uptime & Failover

Even though uptime requirements are quite generous ([Slashing And Penalties](slashing-and-penalties.md)), to keep the maximum performance it is important that your validators are as close to 100% uptime as possible.

Some [validator clients](validator-clients.md) allow for redundant setup, looking at multiple nodes at one time.

See [HA section](ha.md) for more information on failover.


## Read More


