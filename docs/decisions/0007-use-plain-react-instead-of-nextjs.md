[//]: # (bc-madr v0.1)
<!-- modified MADR 4.0.0 -->

# Use plain React instead of Next.js

* status: accepted
* date: 2026-10-01
* decision-makers: Todd Scharien, Hannah MacDonald
* consulted: Marcus Kernohan (Design System Components team)

## Context and Problem Statement

Having already decided to build the portal's frontend with React ([0006](/Users/hamacdonald/LocalDocuments/BCICM/cydb-portal/docs/decisions/0006-use-react-and-javascript-node-to-build-the-portal.md)), we still needed to decide whether to use a React meta-framework such as Next.js, or plain React with no meta-framework.

Should the portal be built with Next.js, or with plain React?

## Decision Drivers

* We want to use [`@bcgov/design-system-react-components`](https://www.npmjs.com/package/@bcgov/design-system-react-components), which is built and tested as plain React components, not with Next.js (e.g., server components, `"use client"` boundaries, SSR hydration) in mind
* We want to avoid mixing a meta-framework with components that were not designed with that framework in mind, to reduce the risk of subtle rendering/hydration bugs and to avoid taking on support burden for an untested combination

## Considered Options

* Next.js
* Plain React

## Decision Outcome

Chosen option: "Plain React", because `@bcgov/design-system-react-components` is built and tested as plain React components and not with Next.js in mind. Mixing a meta-framework like Next.js with components that weren't built for it risks subtle incompatibilities, and we'd rather avoid that risk than gain Next.js's extra features.

### Consequences

* Good, because we avoid the risk of incompatibilities (e.g., SSR hydration issues, server/client component boundaries) between Next.js and `@bcgov/design-system-react-components`, which isn't built or tested with Next.js in mind
* Good, because our stack stays aligned with how the design system components are authored and tested, matching the recommendation from the team that maintains them
* Good, because the frontend architecture remains simpler, with one less framework layer to learn and maintain
* Bad, because we give up Next.js's built-in features (server-side rendering, static generation, file-based routing, API routes, image optimization, etc.) and would need to separately choose/configure tooling for any of these we need
* Neutral, because `@bcgov/design-system-react-components` is still pre-1.0 (major version 0), so we'll need to keep an eye on its releases even though the design system team considers it essentially stable

## Pros and Cons of the Options

### Next.js

* Good, because it provides server-side rendering, static generation, file-based routing, API routes, and other features out of the box
* Good, because it is widely adopted across the broader React ecosystem, with a lot of community support and documentation
* Bad, because `@bcgov/design-system-react-components` is not built or tested with Next.js in mind, risking subtle rendering/hydration bugs
* Bad, because mixing a meta-framework with components not made with that framework in mind increases the risk of incompatibilities and support burden

### Plain React

* Good, because it matches how `@bcgov/design-system-react-components` is built and tested, avoiding framework-mismatch risk
* Good, because it keeps the stack simpler, with no meta-framework-specific conventions to learn or work around
* Neutral, because we lose Next.js's built-in SSR/SSG, routing, and API route features, and would need to separately select tooling for any of these if we need them later
* Bad, because we take on more responsibility for wiring up tooling (bundling, routing, etc.) that a meta-framework would otherwise provide

## More Information

* [`@bcgov/design-system-react-components` on npm](https://www.npmjs.com/package/@bcgov/design-system-react-components)
* [bcgov/design-system](https://github.com/bcgov/design-system)
* [0006 - Use React and JavaScript (Node.js) to build the portal](/Users/hamacdonald/LocalDocuments/BCICM/cydb-portal/docs/decisions/0006-use-react-and-javascript-node-to-build-the-portal.md)
* Decision informed by consultation with Marcus Kernohan from the team maintaining `@bcgov/design-system-react-components`
