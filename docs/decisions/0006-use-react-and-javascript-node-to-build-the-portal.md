[//]: # (bc-madr v0.1)
<!-- modified MADR 4.0.0 -->

# Use React and JavaScript (Node.js) to build the portal

* status: proposed
* date: 2026-09-21
* decision-makers: Todd Scharien, Hannah MacDonald
* consulted: Marcus Kernohan (Design System Components team)

## Context and Problem Statement

We needed to choose the primary UI framework and language/tooling ecosystem for building the CYDB portal's frontend.

What frontend framework and language/runtime ecosystem should we use to build the portal?

## Decision Drivers

* Availability of a public BC Gov npm package ([`@bcgov/design-system-react-components`](https://www.npmjs.com/package/@bcgov/design-system-react-components)) providing a library of pre-built React components implementing BC Gov's design system, reducing UI development effort and ensuring visual/UX consistency with other BC Gov applications
* Broad internal familiarity with React and JavaScript/Node.js among BC Gov developers, reducing onboarding time and increasing the pool of people who can maintain the portal going forward
* Desire to keep consistency with the framework used by [bcgov/caregiver-portal](https://github.com/bcgov/caregiver-portal), which is also built with React and JavaScript/Node.js

## Considered Options

* React with JavaScript/Node.js
* No other options were considered

## Decision Outcome

Chosen option: "React with JavaScript/Node.js", because it has a BC Gov npm package of pre-built, BC Gov-styled React components, a lot of people internally already use and know React and JavaScript/Node.js, and it keeps us consistent with the framework used by the similar [bcgov/caregiver-portal](https://github.com/bcgov/caregiver-portal) project.

### Consequences

* Good, because we can reuse pre-built, BC Gov-styled React components from `@bcgov/design-system-react-components` instead of building UI components from scratch
* Good, because although `@bcgov/design-system-react-components` is in major version 0, we confirmed with Marcus Kernohan (from the team behind this project) that it is essentially stable.
* Good, because the portal's UI will be visually and behaviourally consistent with other BC Gov applications built on the same component library
* Good, because broad internal familiarity with React and JavaScript/Node.js makes it easier to find contributors and reduces onboarding time
* Good, because it keeps us consistent with the framework used by [bcgov/caregiver-portal](https://github.com/bcgov/caregiver-portal), which may make it easier to share knowledge, patterns, or code between the two
* Neutral, because we are committed to the JavaScript/Node.js ecosystem's release cadence and tooling (npm, bundlers, etc.) for the frontend

## More Information

* [`@bcgov/design-system-react-components` on npm](https://www.npmjs.com/package/@bcgov/design-system-react-components)
* [bcgov/design-system](https://github.com/bcgov/design-system)
