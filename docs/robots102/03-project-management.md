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


### Single Responsibility

### Pull Requests

One of the most 

## Automation

Tools which enforce good practices!

### CI/CD

Although it's usually abbreviated as purely CI/CD, Continuous Integration, Continuous Deployment is the practice of software being automatically built (CI) and deployed (CD) at all times.
Every time you push to a branch, your CI pipeline will build it.
Then, once it's built, CD will automatically deploy it.
In the case of this very docs website, CI always runs, but CD only runs on the main branch.

### Branch Protection

Branch protection app