[//]: # (bc-madr v0.1)
<!-- modified MADR 4.0.0 -->

# Choose an authentication strategy

* status: proposed
* date: 2026-10-01
* decision-makers: Todd Scharien, Hannah MacDonald

## Context and Problem Statement

The portal needs a way to authenticate its users.

What authentication strategy should we use for the portal?

## Decision Drivers

* Desire to use a BC Gov-standard, centrally managed identity solution rather than building and operating our own authentication system
* Availability of [Common Hosted Single Sign-on (CSS)](https://bcgov.github.io/sso-docs/), BC Gov's managed Keycloak-based SSO offering, with existing documentation and support
* Ability to authenticate users via the BC Services Card as an identity provider

## Considered Options

* Common Hosted Single Sign-on (CSS) / Keycloak
* No other options were considered

## Decision Outcome

Chosen option: "Common Hosted Single Sign-on (CSS) / Keycloak", because it is BC Gov's standard, centrally managed SSO offering, meaning we don't need to build or operate our own authentication system, and it lets us authenticate users via the BC Services Card.

### Consequences

* Good, because we can use the BC Services Card to authenticate users
* Good, because we offload the operation and maintenance of the identity/authentication infrastructure to the CSS team
* Good, because CSS is well documented and already used across BC Gov, making it easier to find support and examples
* Neutral, because we take on a dependency on the CSS team's roadmap, configuration process, and availability

## More Information

* [Common Hosted Single Sign-on (CSS) documentation](https://bcgov.github.io/sso-docs/)
