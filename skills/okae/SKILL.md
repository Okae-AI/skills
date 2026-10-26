---
name: okae
description: Use when setting up Okae for a GitHub organisation, configuring repository review policy, or verifying an Okae assessment.
---

# Okae

Okae checks PR evidence with mandatory rules, then model judgments when no rule matches.
It routes a PR to human review or approval. A shadow pilot posts the judgment without
submitting PR approvals or merging anything. Service access is based on the repository
owner, not the PR author. Contributors don't need individual Okae accounts or seats.

## Set up the organisation

Ask which GitHub organisation and repository to use and whether the team wants shadow
mode or PR approvals. An organisation owner signs in, connects the workspace and installs
the GitHub App with access to the agreed repository. Guide them through the dashboard's
guided setup and check its real balance and readiness. One PR costs one credit; reassessments
of that PR are free. Don't invent a balance or claim setup is complete without a published result.

## Choose repository settings

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

## Install and verify

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
