# Provisioning Consensus Layer (Checkpoint Sync)

First, it is important to note that provisioning consensus layer via snapshots
of data folder is a bad practice. Multiple nodes might end up with the same
node ID, and that will bring issues during peers discovery (only one node with
a certain ID could be connected to the peers).

Good news, is that all CL nodes have a cross-compatible way of syncing quickly:
**checkpoint sync**. What it does, is it takes the latest blockchain state from
another node (or a file) and applies it w/o doing all the necessary checks.
**Only use trusted source nodes for Checkpoint sync!**.

* Lighthouse: [https://lighthouse-book.sigmaprime.io/checkpoint-sync.html](https://lighthouse-book.sigmaprime.io/checkpoint-sync.html)
* Lodestar: (use `--checkpointSyncUrl`, see [https://chainsafe.github.io/lodestar/reference/cli/)](https://chainsafe.github.io/lodestar/reference/cli/))
* Nimbus: [https://nimbus.guide/trusted-node-sync.html](https://nimbus.guide/trusted-node-sync.html)
* Prysm: [https://docs.prylabs.network/docs/prysm-usage/checkpoint-sync](https://docs.prylabs.network/docs/prysm-usage/checkpoint-sync)
* Teku: [https://docs.teku.consensys.net/en/latest/HowTo/Get-Started/Checkpoint-Start/](https://docs.teku.consensys.net/en/latest/HowTo/Get-Started/Checkpoint-Start/)


**Your Own Checkpoint Sync**

You can checkpoint-sync from any up-to-date CL node, that has beacon API enabled.

[samcm/checkpointz](https://github.com/samcm/checkpointz) is a tool that allows you to setup your own checkpoint sync endpoint and make it public if needed.

**Public Checkpoint Sync Endpoints**

[Community-maintained list of public checkpoint sync services](https://eth-clients.github.io/checkpoint-sync-endpoints/) -- use it if you don't have your own checkpoint sync endpoints or have no up-to-date consensus layer nodes.

When syncing from one of the public sources, always validate that your node is synced to the correct chain. Use [this article](https://notes.ethereum.org/@launchpad/checkpoint-sync#Step-4) to learn how to do that.

In Prysm you can also use `—-weak-subjectivity-checkpoint` flag (read more [here](https://docs.prylabs.network/docs/prysm-usage/parameters)).

**Checkpoint Sync From A File**

For most of the CL nodes, you can store the latest state of the network into
a file, in SSZ format and use that instead of another node. That is useful if
you don't have any trusted node or you have to recreate the setup after it
being completely lost.

Most of the nodes require both the latest finalized state and the block corresponding to the finalized state.

A good practice is to keep these files upgraded once every week.

How to create these files, you can read here: [“Sync from checkpoint files” in Nimbus Guide](https://nimbus.guide/trusted-node-sync.html#sync-from-checkpoint-files). The files obtained there are cross-node compatible.

