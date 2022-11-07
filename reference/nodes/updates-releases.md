# Updates & Releases

## Upgrading Nodes

Upgrading nodes in time is important for two reasons.

Firstly, there are security issues that are fixed in the nodes all the time.

Secondly, it is important to keep track of the hardforks. If hardfork comes and your node is not upgraded, it will use the wrong chain fork.

## How To Stay Up-To-Date?

Most of the nodes are on GitHub. There is [a feature to notify of new releases](https://docs.github.com/en/account-and-profile/managing-subscriptions-and-notifications-on-github/managing-subscriptions-for-activity-on-github/viewing-your-subscriptions). Also you can use this [Slack bot](https://github.com/nightskylark/github-releases-slack-notifier) that notifies about new releases of software.

## Where to track updates?

There are the official channels to follow on Twitter or other places, to be aware of new releases, bugs and features.

* [Nodes: Execution Layer](el/updates.md)

* [Nodes: Consensus Layer](cl/updates.md)

* [Validator Clients](validator-clients/updates.md)

**Hardforks & Other Information**

* EthStaker
    * Twitter: [https://twitter.com/ethstaker](https://twitter.com/ethstaker)
    * Reddit: [https://reddit.com/r/ethstaker](https://reddit.com/r/ethstaker)
    * Discord: [http://invite.gg/ethstaker](http://invite.gg/ethstaker)

* The Ethereum Foundation
    * Twitter: [https://twitter.com/ethereum](https://twitter.com/ethereum)
    * Blog: [https://blog.ethereum.org](https://blog.ethereum.org)


## Nodes: Upgrade Strategies

**Canary Nodes**

Since new releases of nodes can contain bugs, and often critical ones, it is important not to upgrade all nodes at once. 

Good practice is to have “canary” nodes that are upgraded first and monitored for a couple of days (important to get the node through at least one restart through the process, in the past there were cases when the data corruption was only visible after restarts).

If canary nodes show no regressions after 3-7 days, all nodes are upgraded to the new release.

Always keep at least one backup of the node data from the previous build to be able to downgrade! Sometimes nodes update the format of embedded database and after migration it is impossible to go back.

## Node Health After Upgrades

It is important to check the performance characteristics of the nodes after
upgrading. For the specific metrics to track, see [Monitoring](monitoring.md).

When using canary nodes or rolling updates, make sure to keep upgraded nodes to
a separate group in your [monitoring system](monitoring.md), so you can compare
baseline parameters, such as participation rates, resource usage, etc.


## Servers: Harware & Software


Channels to listen to for updates, hard forks, attack mitigations
How to do rolling updates? Go offline for updates?
How often to do updates? When to know an update is urgent?
How to rollback an update? How do know what update needs to be rolled back (what metrics to check)?
How to get rid of a node and start fresh if an update corrupted a DB?
Patch management for OS/Hardware?
