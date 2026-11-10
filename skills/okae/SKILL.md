---
name: okae
description: >
  Use to set up Okae from a checkout, choose repository policy, interpret an
  assessment, or plan changes for review in a team that uses Okae.
---

# Set up and deliver with Okae

Okae checks PR evidence with enabled review rules and protected paths, then model judgments when no rule matches.
It returns an Approve or Review assessment. In shadow mode it publishes the assessment
without submitting a GitHub approval. Okae doesn't merge or deploy. An Approve result
means no concern was identified under the configured policy and available evidence;
it doesn't establish correctness or security. Contributors don't need individual Okae
accounts or seats.

## Read the live docs

Use the [Okae documentation index](https://docs.okae.ai/llms.txt) to find the current
guidance relevant to the task. Read targeted pages rather than the whole site. The skill
provides delivery patterns; the docs explain the current product and configuration.

| Task | Start here |
| --- | --- |
| Understand Okae and set up a repository | [Getting started](https://docs.okae.ai/docs), [GitHub App](https://docs.okae.ai/docs/github) |
| Understand review policy and settings | [Configuration](https://docs.okae.ai/docs/configuration), [configuration workflow](references/configuration.md) |
| Install the App or troubleshoot an assessment | [Troubleshooting](https://docs.okae.ai/docs/troubleshooting), [bundled installation and verification](references/installation.md) |

The docs own setting definitions and current product behaviour; bundled references guide
the workflow. If live docs are unavailable, inspect existing configuration and available
dashboard values, say what remains unverified and defer edits that depend on an unknown
schema. Don't invent accepted settings or current product details.

## Deliver changes

Start with the outcome the user wants and the repository's instructions. Inspect the
parts of the code and tests needed to deliver it, then identify changes that can stand
alone and those that must be reviewed together. Preserve the user's scope and workflow.

Choose PR boundaries for a coherent, safe solution. Keep implementation, tests and
other dependent changes together when they only make sense together. When a larger task
has independently useful pieces, consider delivering them separately; explain their
dependencies and order. Each PR should work on its own and give reviewers the evidence
they need. Don't split work merely to stay below review limits, move sensitive changes to
different paths, or change policy to avoid review.

Use the team's policy to anticipate review and make handoffs clear. For example, explain
that a necessary permission change will need a person if it touches a protected path.
Where relevant and available, check effective settings and approval blockers in the
dashboard and `okae.yml` at the PR head. File values can override saved defaults, and
the dashboard previews the default branch. If effective settings aren't available, say
what remains unknown; the published assessment determines the route for the actual PR.

For a concrete request, choose the suitable shape and proceed under the user's and
repository's permissions. Explain a multi-PR plan when it matters; don't turn a simple
task into a planning exercise. Keep PR titles and descriptions clear about the change,
its purpose, evidence and dependencies so reviewers can make an informed decision.

## Set up Okae

Start in the user's checkout. Identify the repository from its Git remote, or ask which
one they mean if the checkout is ambiguous. Follow [agent installation and browser
handoff](references/installation.md) to run `okae init` with the installed CLI, or via npx if the user prefers to skip installation, and
resume an existing workspace. The owner can also start in the dashboard and hand the
selected repository back to you.

Read the effective policy with `okae config show --json`. Use the
[configuration workflow](references/configuration.md) to recommend changes that fit
this repository. Keep existing policy when it fits. Ask the owner about consumers,
sensitive paths and approval preferences that the checkout cannot establish.

Setup ends when the owner’s choices are effective. If a file change still needs to
land, identify it. Offer a real assessment separately. Let the owner select the PR
before starting a run that can spend a credit.

## Deliver and verify

Treat the expected route as a prediction until Okae assesses the actual PR head. A small
PR may still need human review because of its content or assessment. An approval also
depends on effective settings and service gates; don't promise one or change policy to
obtain one. A shadow result isn't an approval and Okae doesn't merge PRs.

Inspect the published result and assessed version when available. If Okae requests human
review, explain the reason and leave the relevant work for review; don't edit unrelated
code to make the check green. For an error or missing assessment, use the troubleshooting
guidance in [installation and verification](references/installation.md). Follow the team's
branch protections and authorization for opening, updating and merging PRs.
