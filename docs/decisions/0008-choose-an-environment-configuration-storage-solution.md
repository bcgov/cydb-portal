[//]: # (bc-madr v0.1)
<!-- modified MADR 4.0.0 -->

# Choose an environment configuration storage solution

* status: proposed
* date: 2026-10-01
* decision-makers: Todd Scharien, Hannah MacDonald

## Context and Problem Statement

The portal needs a way to store environment-specific configuration, both sensitive (secrets) and non-sensitive (config), that varies between environments (e.g., dev, test, prod) and gets supplied to the running containers.

Should we use HashiCorp Vault, or OpenShift secrets and config maps, to store this environment-specific configuration?

## Decision Drivers

* Setup and ongoing operational complexity of Vault (authentication methods, policies, integration tooling) versus OpenShift secrets/config maps, which are native, built-in OpenShift objects
* OpenShift secrets and config maps can automatically populate container environment variables natively (e.g., via `envFrom`/`secretKeyRef`), whereas Vault requires additional integration to get values into a container's environment
* We decided not to set up disaster recovery (DR) ([ADR-0005](./0005-decide-on-using-disaster-recovery-on-gold.md)), so we don't have parallel environments/clusters that would benefit from having secrets centralized in one place, which removes one of the main advantages Vault would otherwise offer
* Ability for the current team to build, learn, and maintain the solution

## Considered Options

* Use HashiCorp Vault
* Use OpenShift secrets and config maps

## Decision Outcome

Chosen option: "Use OpenShift secrets and config maps", because Vault is more complex to set up and interact with, doesn't automatically populate containers with environment variables the way OpenShift secrets/config maps do out of the box, and because we aren't setting up DR, we don't get the benefit of having secrets for parallel environments stored in one place, which may otherwise have justified Vault's added complexity.

### Consequences

* Good, because secrets and config maps are native OpenShift objects, requiring no additional service to set up, authenticate against, or maintain
* Good, because secret/config map values automatically populate container environment variables without anything extra required
* Good, because it reduces the operational and learning overhead for the current team
* Neutral, because configuration remains scoped per environment/cluster rather than centralized in one place
* Bad, because we give up Vault features such as dynamic/rotating secrets, fine-grained access policies, and centralized audit logging

## Pros and Cons of the Options

### Use HashiCorp Vault

* Good, because it can centralize secrets across multiple environments/clusters in one place
* Good, because it supports dynamic secrets, automatic rotation, fine-grained access policies, and centralized audit logging
* Bad, because it is more complex to set up and interact with (authentication methods, policies, integration tooling)
* Bad, because it doesn't automatically populate container environment variables; an additional integration is needed
* Bad, because without DR or other parallel environments/clusters, we don't benefit from Vault's main advantage of centralizing secrets in one place

### Use OpenShift secrets and config maps

* Good, because they are native, built-in OpenShift objects requiring no additional service to set up or maintain
* Good, because they automatically populate container environment variables out of the box
* Good, because they are simpler to learn and interact with for the current team
* Neutral, because configuration stays scoped per environment/cluster rather than centralized
* Bad, because they lack Vault's more advanced features, such as dynamic secrets, automatic rotation, and centralized audit logging

## More Information

* [ADR-0005 - Decide on using disaster recovery (DR) on the Gold hosting tier](./0005-decide-on-using-disaster-recovery-on-gold.md)
