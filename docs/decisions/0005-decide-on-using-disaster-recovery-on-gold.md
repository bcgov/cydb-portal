[//]: # (bc-madr v0.1)
<!-- modified MADR 4.0.0 -->

# Decide on using disaster recovery (DR) on the Gold hosting tier

* status: proposed
* date: 2026-09-21
* decision-makers: Todd Scharien, Hannah MacDonald
* consulted: Jonathan Sharman (Keycloak team)

## Context and Problem Statement

Having chosen the OpenShift Gold hosting tier ([ADR-0004](./0004-select-a-hosting-platform.md)), Gold supports an optional geographic failover to a Gold DR cluster in Calgary, which raises platform availability but requires additional infrastructure and operational work to configure.

Should we set up disaster recovery (DR) failover for the CYDB portal on Gold, or run on Gold without DR?

## Decision Drivers

* Desire for higher availability in the event of a Kamloops data centre outage
* Implementation and ongoing maintenance effort required versus the actual availability gain
* Complexity of replicating stateful data (databases) between clusters
* Ability for the current team to build and maintain the solution

## Considered Options

* Set up disaster recovery (DR) failover to Gold DR (Calgary)
* Use Gold without DR

## Decision Outcome

Chosen option: "Use Gold without DR", because after consulting Jonathan Sharman on the Keycloak team and reviewing [bcgov/sso-switchover-agent](https://github.com/bcgov/sso-switchover-agent) (the tooling used to run Gold DR failover for Keycloak), we determined that building and maintaining a DR setup could take months of effort for only a small service availability gain (99.95% with DR vs. 99.5% without, equivalent to a few hours, per BC Gov's [hosting tiers documentation](https://digital.gov.bc.ca/technology/cloud/private/products-tools/hosting-tiers/)). It also becomes substantially more complex once a database is involved, since data hydration and rehydration between clusters on Patroni is not easy to get right.

### Consequences

* Good, because it avoids the significant implementation and ongoing maintenance effort required to build and operate DR/switchover tooling
* Good, because it avoids the complexity of replicating and rehydrating database data between clusters on Patroni
* Neutral, because we still benefit from Gold's delayed upgrade cycle even without DR
* Bad, because in the event of a full Kamloops data centre outage, the portal will be unavailable until the Gold cluster recovers, with no automatic failover

## Pros and Cons of the Options

### Set up disaster recovery (DR) failover to Gold DR (Calgary)

* Good, because it raises platform availability to 99.95% via automatic failover to Calgary
* Good, because it minimizes downtime during a Kamloops data centre outage
* Bad, because implementing and maintaining a DR/switchover setup similar to `sso-switchover-agent` is estimated to take months of effort
* Bad, because it requires a GSLB (global server load balancer) service and multi-node deployment configuration
* Bad, because it becomes substantially more complex once a database is involved, as Patroni data hydration and rehydration between clusters is difficult
* Bad, because it introduces ongoing operational burden, such as monitoring failover state and performing manual failback steps

### Use Gold without DR

* Good, because it requires no additional failover tooling or GSLB configuration
* Good, because it avoids the complexity of cross-cluster database replication
* Good, because we still get Gold's delayed upgrade cycle
* Bad, because availability remains at 99.5% rather than 99.95%, with no automatic recovery from a Kamloops outage
