# Monitoring

**Monitoring** is what metrics to keep track of when running validators.

Usually it is good to monitor for a lot of things, including normal ops metrics and blockchain-specific metrics.

### EthereumPools

There are services offering external monitoring of validator performance.

One of them is [EthereumPools.info](https://ethereumpools.info/). You can
contact the authors to add your own pool of validators there and get some
public metrics there and be contacted for extra information.

To get your nodes monitored, contact via Twitter [twitter.com/ethereumPools](https://twitter.com/ethereumPools).

### Beaconcha.in Mobile App

* [Beaconcha.in Mobile App](https://kb.beaconcha.in/beaconcha.in-explorer/mobile-app-less-than-greater-than-beacon-node) allows monitoring your validators one-by-one and also alerts you when something goes wrong.

### Grafana

[Grafana dashboard for validators](https://grafana.com/grafana/dashboards/13481-eth-validators/). This one looks like it wasn’t touched for a long time, so it might not be a good “out of the box” solutions, but might be a first step towards your own dashboard with the data you need.

[RocketPool Grafana Dashboards for nodes](https://docs.rocketpool.net/guides/node/grafana.html#importing-the-rocket-pool-dashboard). Rocket Pool provides multiple dashboards for different types for [nodes](nodes.md) and [validator clients](validator-clients.md)

**Client Teams Dashboards**

* [Prysm Grafana Dashboard](https://docs.prylabs.network/docs/prysm-usage/monitoring/grafana-dashboard)

* [Lighthouse Grafana Dashboards](https://github.com/sigp/lighthouse-metrics)

* [LodeStar Grafana Metrics](https://chainsafe.github.io/lodestar/usage/prometheus-grafana/)

* [Nimbus Grafana Dashboard](https://nimbus.guide/metrics-pretty-pictures.html)

* [Teku Grafana Dashboard](https://docs.teku.consensys.net/en/latest/HowTo/Monitor/Metrics/)

### Eth2 Monitor (StakeFish)

[Eth2 Monitor](https://github.com/stakefish/eth2-monitor) from StakeFish not only monitors attestation performance with Slack integration, it also allows to look up for a maintenance window of 6.4 minutes (1 epoch size). This maintenance window means during the next epoch there will no be block proposals from these validators so you don't lose the slot.

### DataDog

[DataDog](https://www.datadoghq.com) is a SaaS for monitoring and alerting. It has a prometheus-compatible APIs to scrape data from hosts, so you can use the same metrics from the nodes or from the validator clients.


## Further Reading

Want to learn more? Here are some articles you might find useful.

* [Alerting & Incident Response](alerting.md)

* [Monitoring Ethereum Staking Infrastructure At Scale](https://www.kiln.fi/post/monitoring-ethereum-staking-infrastructure-at-scale) by Kiln.
