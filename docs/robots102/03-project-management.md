# Project Management

This lesson will cover some of the most common ways projects are managed in modern software, as well as the development patterns and terminology associated with that.

## Terminology

A lot of terminology is going to get thrown around in this lesson!
Much of it requires understanding version control, which the [previous lesson](./02-version-control.md) covers.
If you're confused, you might be missing a term or concept covered there.

## Prerequisites

Follow the prerequisites in the [previous lesson](./02-version-control.md) so that you have everything you need already set up.

## Development Principles

### Short-Lived Branches

To ensure that no branch ever diverges too far from the main codebase, branches should typically be reviewed and merged in a fairly short timeframe.
Ideally, each branch only lasts a few days to a couple of weeks at most.

### Single Responsibility Branches

Each branch should also normally be dedicated to a single purpose.
This might be a bugfix, feature implementation, or random experiment.
Either way, you should try to ensure that whatever you're working on is a small enough unit of work that it _can_ be developed in the short timeframes specified above.
Following this practice also ensures that pull requests are much easier to review when the time comes, since each one should be a small, self-contained, and focused set of changes.

### Pull Requests

## Automation

Tools which enforce good practices!

### Continuous Integration

Continuous Integration is a way of developing software which requires _continually_ pushing commits to the remote server so that it can be built.

### Continuous Deployment

Continuous Deployment (CD) builds on top of CI, and refers to tooling which automatically deploys your software.
In the case of this very docs website, its CD pipeline automatically builds and uploads it to the website whenever it gets pushed to the `main` branch.

### Branch Protection
