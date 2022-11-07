# Provisioning/Scaling Execution Layer

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
