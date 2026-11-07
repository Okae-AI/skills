---
name: okae
description: >
  Use when delivering changes in a repository using Okae, understanding an
  assessment, or setting up Okae and its repository review settings.
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

## Find the useful shape

Follow the part of this skill that fits the request. For delivery, work from the
desired outcome and the team's review process. For onboarding, guide the user through
hosted setup, optional configuration and a real assessment. Resume from their current
progress rather than repeating completed steps.

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

Read [installation and verification](references/installation.md) and the relevant live
docs before guiding setup. Identify the repository and GitHub organisation from available
context; ask only for missing choices. Explain that setup needs an organisation owner
and selected-repository GitHub App access. Personal-account repositories aren't supported.

Start at [app.okae.ai](https://app.okae.ai). Guide the user through GitHub sign-in,
organisation connection, agreement acceptance and App installation. These hosted steps
establish account access and processing authority. The skill supplies guidance, not an
authenticated connection: public Okae CLI and MCP operations aren't available. Don't
invent commands or ask the user to paste session cookies or tokens.

Leave GitHub sign-in, contractual acceptance and permission grants to an authorised person.
Explain each next step and continue when they return. If the App is already installed,
help complete the existing connection rather than reinstalling it. Use available dashboard
evidence or ask what the user sees; distinguish their report from checks you observed.

In Getting started, choose the repository, help select a configuration approach and check
readiness. Start new setups in shadow mode. Preserve an existing approval policy unless
the team agrees to change it. The dashboard can provide a repository-specific agent prompt
and a return link to verification; use that context when supplied. Check actual service
readiness and credit balance without inventing values. Use the live credits docs for
pricing and billing questions rather than requiring a purchase to begin.

### Choose repository settings

Read the [current configuration guide](https://docs.okae.ai/docs/configuration) and use
the [configuration workflow](references/configuration.md) when creating, changing or
explaining policy. Inspect the repository's own agent instructions, directory
structure, manifests, review policies and existing config. Identify the actual repository;
ask when the intended target is unclear.

Explain the choices: use valid existing defaults, edit repository defaults in the dashboard,
or write `okae.yml` for settings reviewed and versioned with the code. Explicit file values
override saved repository defaults. A file is optional. Recommend a choice based on the
team's needs and don't change policy without their agreement.

Walk through the settings with the owner using the [configuration workflow](references/configuration.md).
Explain the automatic review triggers and use examples from their repository. Keep defaults
unless they choose changes, and keep new setups in shadow mode. A walkthrough can end with
using defaults; it doesn't require creating a file or changing every setting.

When the user chooses a file, inspect existing settings and propose a small config using real
repository paths. Explain protected paths and ask about uncertain policy. Create or update
root-level `okae.yml`, preserve unrelated settings, show the diff and follow repository rules.
Ask before pushing, opening a PR or merging unless the user has already authorised that action.

Check YAML syntax and supported keys, types and ranges with available tooling. There is
no bundled official validator or config simulator. Distinguish a static check from a live
Okae result. Keep credentials and service-level settings out of repository config.

### Install and verify

Use [installation and verification](references/installation.md) when checking an
installation or diagnosing a missing result. Okae runs as a hosted GitHub App; the
customer doesn't deploy its service in their repository.

Verify installation, dashboard readiness, a published assessment and the dashboard's setup
completion. Installing the
skill or creating YAML doesn't establish service readiness. PR assessments use the file in
the assessed head commit. Changes to `okae.yml` require human review. The dashboard settings
view previews the default branch, which can differ from the PR head.

Keep human review and existing branch protections. Check the effective
`enable_approvals` setting and its source for shadow mode. If the team explicitly requests
approvals, confirm the effective setting and service approval availability. A human-review outcome is expected routing, not
an instruction to edit application code. For processing errors, collect the PR link,
time and error ID rather than trying to make the check green through unrelated edits.

Finish with the config changes, checks actually performed and remaining installation or
verification steps. Collect disagreements per PR, keeping the assessed version when needed.

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
