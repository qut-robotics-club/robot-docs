# Project Management

This lesson will cover some of the most common ways projects are managed in modern software, as well as the development patterns and terminology associated with that.

## Terminology

A lot of terminology is going to get thrown around in this lesson!
Much of it requires understanding version control, which the [previous lesson](./02-version-control.md) covers.
If you're confused, you might be missing a term or concept covered there.

## Prerequisites

Follow the prerequisites in the [previous lesson](./02-version-control.md) so that you have everything you need already set up.

## Development Principles

Some of the most important principles to making all of these concepts work.

### Short-Lived Branches

To ensure that no branch ever diverges too far from the main codebase, branches should typically be reviewed and merged in a fairly short timeframe.
Ideally, each branch only lasts a few days to a couple of weeks at most.

### Single Responsibility Branches

Each branch should also normally be dedicated to a single purpose.
This might be a bugfix, feature implementation, or random experiment.
Either way, you should try to ensure that whatever you're working on is a small enough unit of work that it _can_ be developed in the short timeframes specified above.
Following this practice also ensures that pull requests are much easier to review when the time comes, since each one should be a small, self-contained, and focused set of changes.

## Pull Requests

A Pull Request (or PR) is a mechanism used in VCS's to request that changes made in one branch be merged into another (usually `main` or `master`).
It allows team members to review, discuss, and approve or reject code changes before they become part of the main codebase.

**Typical Workflow:**

1. Create a new branch for your work, dedicated to a specific purpose.
2. Commit changes on that branch and push changes to the remote repository.
3. Open a Pull Request against the target branch (normally `main`).
4. Team members review, leave comments, and request modifications if needed.
5. Once approved and all checks pass, the PR is merged into the main branch.

### Why Use Pull Requests?

Pull Requests are essential for maintaining code quality in collaborative development environments - or even on your own!
They serve several main purposes:

- **Code Review:** Team members can review changes before they're merged to catch bugs, ensure a consistent style, and maintain high-quality code.
- **Automated Tooling:** CI pipelines can automatically run formatting and linting tools, check for easily-detectable issues, and automatically enforce development rules.
- **Knowledge Sharing**: When developers review each other's code, they learn about different approaches and best practices.
- **Documentation:** A well-written PR description documents _why_ a change was made, not just _what_ changed.
  This becomes particularly important for longer-running projects, where the reason for a change may not be so obvious later down the line.
- **Security:** Security issues can be caught before reaching production.

## Automation

Tools to enforce good practices!

### Continuous Integration

Continuous Integration (CI) is a development approach which requires _regularly_ pushing commits to the remote repository, triggering automated builds and tests.

**Benefits of CI:**

- Catches integration issues early
- Provides fast feedback on build failures
- Ensures the codebase remains in a deployable state at all times

**Typical Pipeline Steps:**

1. Checkout that branch's code
2. Run linting and formatting checks
3. Execute automated tests
4. Build the application
5. Upload artifacts (built outputs) or notify of failures

Technically linting, formatting, and testing are all optional, but they are some of the most important reasons to build a CI pipeline to start with!
For example, this repo's CI pipeline automatically checks for typos and will reject deployment if there are any.

### Continuous Deployment

Continuous Deployment (CD) builds on top of CI by automatically _deploying_ your software to production when it passes all checks.
In the case of this very docs website, its CD pipeline automatically uploads it to the website whenever changes get pushed to the `main` branch.

!!! note
    Not all projects need to, or should, use full Continuous Deployment!
    Some use Continuous Delivery, which is very similar, but requires manual approval first.

**Caveats:**

- The deployment process must be idempotent (safe to run multiple times).
- Initial deployments should be closely monitured until they're thoroughly proven.

### Branch Protection Rules

Branch protection rules enforce best practices on the repository level, and on GitHub are part of the repository settings.
Some of the most important include:

- **PR Reviews**: Configure how many reviews are needed before merging (e.g. 1 or 2).
- **Passing Status Checks**: Ensure CI/CD completes successfully before allowing PRs to merge.
- **Preventing Direct Pushes**: Block direct commits by protecting branches like `main` or `master`.
- (Optionally) **Enforcing Linear History**: Force rebasing to maintain a clean commit history.

Relying on the CI/CD pipeline status ensures that the code will (hopefully) never be broken, especially if it includes testing, and requiring reviews can enforce that at least one other person has read the code before it gets merged.
Preventing direct pushes to the main branch means that the code can only be modified through pull requests, which enforces all the other rules for _everybody_.
Finally, linear history is an optional nice-to-have which some projects like, since it can make the commit history easier to navigate.

## Code Review Etiquette

When reviewing a PR:

- **Deal with the biggest issues first:** Security issues, logic errors, and the like.
- **Leave actionable comments:** Give both a suggested path of action where applicable, and explain _why_ a change should be made.
- **Don't nitpick style:** Wherever possible, style should be enforced by automated linting and formatting tools.
  Only overall code style that can't be automatically linted should be manually and commented on.
- **Approve PRs quickly:** Try to review small, focused PRs quickly so they can be merged and unblock developers.

Additionally, when requesting changes:

- **Be polite.** Remember, at the end of the day, a human is responsible for the code you're reviewing.
- Try to give _constructive_ criticism.
- Reference specific lines or commits. In GitHub, PR comments can be linked to specific ranges of code, so you have no excuse!
- Explain the impact of your concern.

## Merge Conflicts

Merge conflicts occur when two branches have changed the same section of code.
They're common and expected in collaborative development.
However, the less often they occur, the better!
This is one of the biggest reasons to keep branches short-lived, as it drastically reduces the chances of merge conflicts.

**How to Resolve:**

1. Pull the latest changes from the main branch into your own.
2. Identify conflicting files (usually marked in your IDE).
3. Review each conflict manually—don't just choose one side!
4. Test **thoroughly** after resolution.
5. Commit and push the resolved version!

### Tips and Tricks

Of course, the best merge conflict is the one that never happened at all.
You can usually mitigate, if not entirely avoid, conflicts with the following practices:

- Update branches frequently - smaller conflicts are much easier to resolve than big ones!
- Use small, frequent commits.
- Avoid working on large features that will take weeks to complete. Try to break it down into smaller chunks that will be quicker to develop.

Although Git uses a specific text-based format to mark merge conflicts, most IDEs (VSCode included) provide a graphical resolution tool to help you through it.
Additionally, programs like `delta` (see [Git setup](./02-version-control.md#making-git-fancy)) can provide a much nicer terminal experience too.
