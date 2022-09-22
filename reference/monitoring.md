# Monitoring & Alerting

**Monitoring** is what metrics to keep track of when running validators.

**Alerting** is what do you want to be notified about from these metrics.

## Monitoring

Usually it is good to monitor for a lot of things.

### EthereumPools

There are services offering external monitoring of validator performance.

One of them is [EthereumPools.info](https://ethereumpools.info/). You can
contact the authors to add your own pool of validators there and get some
public metrics there and be contacted for extra information.

### Self-Hosted Solutions

Grafana, Prometheus

### SaaS

DataDog

## Alerting

Alerting should be very specific. It’s easy to just set thresholds to every possible monitored metric and add alarm to it. But that could lead to fatigue, distractions and also ignoring alerts.

Alerts should never be ignored, even if you think you have an idea what caused them.

For good tips on alerting in general, see [“My Philosophy on Alerting”](https://docs.google.com/document/d/199PqyG3UsyXlwieHaqbGiWVa8eMWi8zzAn0YfcApr8Q/edit).


## Tools for Alerting

SaaS:

* Pager Duty

* VictorOps 

## On-Call

There is a practice in every cloud service, called “being on-call”. That means that at some moment in time there is a person responsible for reacting to alerts, regardless of when they happen.

That means being ready to act in the middle of the night, in the weekends, etc. That is a tedious and tiring position to be in, so it is better to rotate people often on that.

An example of the on-call policy could be found in this [GitLab On-Call Handbook](https://about.gitlab.com/handbook/on-call/).


## Inactivity leaks — have more time

Inactivity leak means your node was chosen to do a certain duty (attesting for the chain head or producing a block) and didn’t do its job in time.

Inactivity leaks have relatively small penalties. They will degrade the performance of the Validator in terms of the yearly yield, but it take a long time for them to 

That means that you have some choice in how to handle them:

1. react ASAP — use if you have a proper DevOps team and you want to optimize the node performance and the best APY possible. Ensure regular rotations in the on-call team.

2. react only during “business hours”, but on weekends — only notify, say, from 9:00 to 21:00 every day. That greatly reduces the strain on the on-call personal.

3. react only during business hours — same as (2) but don’t notify on weekends.


## Delays in attestations (node suboptimal performance)




* Intro to standard beacon API & metrics (ideally we have open sourced dashboards by then)
* Explanation of basic alerts they should incorporate (delayed slots, low participation rate, block processing times, etc)
* How long to store data for?
* Generic recommendation on alerting/metrics best practices

## Incident Response
What to look for first? When do you raise an alarm?
First steps required during incidence response
What channels to reach out if you think its a network attack?
What channels to reach out if its a possible vulnerability?


    - Regular Monitoring
    - On-Call & Alerting
    - Blockchain Events Monitoring
    - Dashboards
