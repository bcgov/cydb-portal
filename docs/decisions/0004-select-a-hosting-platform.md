[//]: # (bc-madr v0.1)
<!-- modified MADR 4.0.0 -->

# Select a cloud hosting platform

* status: accepted
* date: 2026-09-21
* decision-makers: Todd Scharien, Hannah MacDonald

## Context and Problem Statement

We need a place to host and run the CYDB portal frontend. BC Gov's private cloud offers multiple OpenShift clusters, so beyond choosing OpenShift itself, we also need to decide which cluster to deploy to.

## Considered Options

* OpenShift Gold
* OpenShift Silver
* Virtual Machine with Podman
* No alternative cloud services were considered

## Decision Outcome

Chosen option: "OpenShift Gold", because the social-middleware service this project depends on is already hosted on Gold, and co-locating the two on the same cluster simplifies networking and configuration.

### Consequences

* Good, because OpenShift is provided as a free private cloud service to BC Gov at large
* Good, because there is a growing internal community to draw support from
* Good, because of Kubernetes' reliability
* Good, because we can use Helm for Infrastructure as Code
* Good, because we can set up CI/CD for rapid development and easier deployments
* Good, because being on the same cluster as social-middleware avoids cross-cluster networking and firewall configuration
* Bad, because OpenShift can be difficult to learn, making developer onboarding require more effort

## Pros and Cons of the Options

### OpenShift Gold

[More info on the Gold hosting tier](https://digital.gov.bc.ca/technology/cloud/private/products-tools/hosting-tiers/)

* Good, because social-middleware is already hosted there, simplifying networking configuration
* Good, because upgrades and patches are tested on Silver for a week before being applied, reducing the risk of platform-caused disruptions
* Neutral, because it otherwise meets the same Protected B hosting requirements as Silver
* Neutral, because it is functionally equivalent to Silver in terms of OpenShift features and support without setting up DR
* Bad, because configuring DR adds setup complexity if we choose to use it

### OpenShift Silver

[More info on the Silver hosting tier](https://digital.gov.bc.ca/technology/cloud/private/products-tools/hosting-tiers/)

* Good, because it meets the same Protected B hosting requirements as Gold
* Good, because it uses standard OpenShift routing without the extra GSLB/DR setup required for Gold failover
* Bad, because it would require cross-cluster networking to communicate with social-middleware on Gold

### Virtual Machine with Podman

* Good, because deployment is greatly simplified without needing Kubernetes
* Bad, because high-availability is considerably more difficult to implement.