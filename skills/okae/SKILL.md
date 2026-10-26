---
name: okae
description: >
  Use when delivering changes in a repository using Okae, understanding an
  assessment, or setting up Okae and its repository review settings.
---

# Deliver with Okae

Okae checks PR evidence with mandatory rules, then model judgments when no rule matches.
It routes a PR to human review or approval. A shadow pilot posts the judgment without
submitting PR approvals or merging anything. Service access is based on the repository
owner, not the PR author. Contributors don't need individual Okae accounts or seats.

## Read the live docs

Use the [Okae documentation index](https://docs.okae.ai/llms.txt) to find the current
guidance relevant to the task. Read targeted pages rather than the whole site. The skill
provides delivery patterns; the docs explain the current product and configuration.

| Task | Start here |
| --- | --- |
| Understand Okae and set up a repository | [Getting started](https://docs.okae.ai/docs), [GitHub App](https://docs.okae.ai/docs/github) |
| Understand review policy and settings | [Configuration](https://docs.okae.ai/docs/configuration), [bundled configuration reference](references/configuration.md) |
| Install the App or troubleshoot an assessment | [Troubleshooting](https://docs.okae.ai/docs/troubleshooting), [bundled installation and verification](references/installation.md) |

If live docs are unavailable, use the bundled references and available repository
settings, say what you couldn't verify, and avoid inventing current product details.

## Find the useful shape

Follow the part of this skill that fits the request. For delivery, work from the
desired outcome and the team's review process. For onboarding, start with the
organisation, repository and review preferences, then choose settings and verify setup.

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

Ask which GitHub organisation and repository to use and whether the team wants shadow
mode or PR approvals. An organisation owner signs in, connects the workspace and installs
the GitHub App with access to the agreed repository. Guide them through the dashboard's
guided setup and check its real balance and readiness. One PR costs one credit; reassessments
of that PR are free. Don't invent a balance or claim setup is complete without a published result.

### Choose repository settings

Read [the configuration reference](references/configuration.md) when creating, changing
or explaining `okae.yml`. Inspect the repository's own agent instructions, directory
structure, manifests, review policies and existing config. Identify the actual repository;
ask when the intended pilot target is unclear.

Explain the choices: use valid existing defaults, edit repository defaults in the dashboard,
or write `okae.yml` for settings reviewed and versioned with the code. Explicit file values
override saved repository defaults. A file is optional. Recommend a choice based on the
team's needs and don't change policy without their agreement.

When the user chooses a file, inspect existing settings and propose a small config using real
repository paths. Explain protected paths and ask about uncertain policy. Create or update
root-level `okae.yml`, preserve unrelated settings, show the diff and follow repository rules.

Check YAML syntax and supported keys, types and ranges with available tooling. There is
no bundled official validator or config simulator. Distinguish a static check from a live
Okae result. Keep credentials and service-level settings out of repository config.

### Install and verify

Read [installation and verification](references/installation.md) when onboarding a repo,
checking an installation or diagnosing a missing result. Present the App installation URL
and selected-repository steps to the authorised installer. Okae runs as a hosted GitHub
App; the customer doesn't deploy its service in their repository.

Verify installation, dashboard readiness, a published assessment and the dashboard's setup
completion. Installing the
skill or creating YAML doesn't establish service readiness. PR assessments use the file in
the assessed head commit. Changes to `okae.yml` require human review. The dashboard settings
view previews the default branch, which can differ from the PR head.

For a pilot, keep human review and existing branch protections. Check the effective
`enable_approvals` setting and its source for shadow mode. If the team explicitly requests
approvals, confirm the effective setting and the operator's global switch. A human-review outcome is expected routing, not
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
