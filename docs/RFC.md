# CYDB portal

Author(s): Todd Scharien, Sagar Shah

Business area: MCFD Mobility project team

Proposed: 2026-10-07

## Abstract

This document is an overview of a web app for families to access the new Child and Youth Disability Benefit (CYDB).

## Intro

As the Ministry introduces the Child and Youth Disability Benefit (CYDB) in April 2027, families will need a modern, secure, and centralized way to manage their disability benefit services online. Historically, families receiving Autism Funding relied on the My Family Services (MyFS) Portal to apply for services and review financial information. As clients transition to the new CYDB program, MyFS will not be used for CYDB Benefit and will sunset from MCFD side with autism funding program.

The Child and Youth Disability Benefit Portal will become the future digital front door for families receiving CYDB services. Through integration with BC Services Card and ICM, the portal will provide a single, trusted platform where families can securely access and manage their benefit information. Users will be able to view approved funding, monitor benefit utilization and remaining balances, apply for access, submit amendment requests, and manage product authorization requests online.

## ADR overview

We will use a [React web app (0006)](decisions/0006-use-react-and-javascript-node-to-build-the-portal.md) (connected to the [Social middleware](https://github.com/bcgov/social-middleware) backend) to serve users, hosted in [BC Gov's private cloud (0004)](decisions/0004-select-a-hosting-platform.md). Network access to the web app will go through an [OCIO APS reverse proxy (0010)](decisions/0010-choose-a-routing-solution-for-the-portal.md), where we can apply hardening plugins to requests as necessary.

Users will log in using their [BC Services Card (via Keycloak) (0009)](decisions/0009-choose-an-authentication-strategy.md) to access benefits services and their de-identified identifier (DID) will be used to retrieve relevant  information from ICM.

[Disaster recovery (DR) (0005)](decisions/0005-decide-on-using-disaster-recovery-on-gold.md) is not needed for this citizen-facing web app. Expected timelines for benefits fulfillment operate on the scale of weeks. Our chosen private cloud SLA allows for only a few hours downtime per year. If the web app is down for a few hours during the year, we expect downtime to not affect processing meaningfully.

We will use OpenShift-native objects for [environment and secret configuration (0008)](decisions/0008-choose-an-environment-configuration-storage-solution.md)—the benefits for using Vault do not currently outweight its complexity to implement and maintain.

## Design

[Architecture overview](design/architecture.md)

[Sequence diagram - login flow](design/login-sequence.md)