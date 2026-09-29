[//]: # (bc-madr v0.1)
<!-- modified MADR 4.0.0 -->

# Use BC-MADR to record architectural decisions

* status: accepted
* date: 2026-09-21
* decision-makers: Todd Scharien, Hannah MacDonald

## Context and Problem Statement

As the project grows, we need a consistent way to record significant decisions about its direction (architecture, tooling, process, etc.) so that the reasoning behind them isn't lost over time or scattered across chat logs, meeting notes, and cloud documents.

## Decision Drivers

* Want a lightweight, predictable, and repeatable format for recording decisions
* Want decisions to be version-controlled alongside the code they affect
* Want alignment with BC Gov standards where they exist

## Considered Options

* Use BC-MADR
* Use plain MADR
* Use free-form documents (e.g., Word docs, wiki pages, stories)
* Do not formally record decisions

## Decision Outcome

Chosen option: "Use BC-MADR", because it is a BC Gov-endorsed extension of the widely used MADR format, giving us a standardized structure while remaining lightweight enough to keep in the repository alongside the code.

### Consequences

* Good, because decisions are stored as version-controlled Markdown files next to the code they affect.
* Good, because the format is standardized, making records easier to write, read, and compare across projects.
* Neutral, contributors need to learn the BC-MADR/MADR structure and conventions.
* Bad, because it adds a small amount of process overhead when making significant decisions.

## Pros and Cons of the Options

### Use BC-MADR

* Good, because it is a BC Gov-endorsed standard, aligning us with other provincial projects
* Good, because it extends MADR, a well-known and documented format
* Neutral, because it leaves our decisions on the repo and thuis out in the open

### Use plain MADR

* Good, because it is a well-established, widely adopted format
* Bad, because it lacks BC Gov-specific conventions

### Use free-form documents

* Good, because there is no format to learn
* Bad, because records are inconsistent and harder to compare across decisions
* Bad, because documents are typically stored outside of version control
* Bad, because documents can be lost if they are scattered

### Do not formally record decisions

* Good, because there is no overhead
* Bad, because the reasoning behind past decisions is easily lost
