[//]: # (bc-madr v0.1)
<!-- modified MADR 4.0.0 -->

# Choose a routing solution for the portal

* status: proposed
* date: 2026-10-01
* decision-makers: Todd Scharien, Hannah MacDonald

## Context and Problem Statement

The portal needs a way to route external traffic to it. BC Gov offers [API Program Services (APS)](https://digital.gov.bc.ca/bcgov-common-components/api-program-services/), a managed reverse proxy/gateway, as an alternative to routing directly with native OpenShift routes.

Should we route to the portal using APS, or using OpenShift routes?

## Decision Drivers

* Desire for the extra features APS provides as a reverse proxy/gateway
* Certificate management effort: OpenShift routes would require us to source and manage our own TLS certificates, whereas APS handles this for us
* Ability for the current team to build and maintain the solution

## Considered Options

* Use API Program Services (APS)
* Use OpenShift routes

## Decision Outcome

Chosen option: "Use API Program Services (APS)", because it gives us extra reverse proxy features like rate limiting, and it avoids the need to source and manage our own TLS certificates, which we would otherwise need to do with OpenShift routes.

### Consequences

* Good, because we gain access to APS's additional reverse proxy features
* Good, because we don't need to source, install, or renew our own TLS certificates
* Neutral, because we take on a dependency on the APS platform and its configuration/onboarding process
* Bad, because it adds an additional managed component in front of the portal, compared to routing directly with a native OpenShift route

## Pros and Cons of the Options

### Use API Program Services (APS)

* Good, because it provides extra reverse proxy features like rate limiting that we wouldn't get with just an OpenShift route
* Good, because it manages TLS certificates for us, so we don't need to source or maintain our own
* Bad, because it introduces an additional managed component/dependency in front of the portal

### Use OpenShift routes

* Good, because it is a simpler, native OpenShift solution with nothing extra to onboard or configure
* Bad, because it lacks the extra reverse proxy features APS provides
* Bad, because we would need to source and manage our own TLS certificates

## More Information

* [API Program Services (APS)](https://digital.gov.bc.ca/bcgov-common-components/api-program-services/)
