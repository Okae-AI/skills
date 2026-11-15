---
name: okae
description: >
  Use to set up Okae, interpret assessment history, decide what a team wants
  to delegate, tune repository policy, or plan, check and open PRs in a repo
  that uses Okae.
---

# Set up and deliver with Okae

Okae assesses a PR revision against the repository's policy.
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
| Run a preflight before a PR or add an agent hook | [Use Okae with a coding agent](https://docs.okae.ai/docs/cli#use-okae-with-a-coding-agent) |

The docs own setting definitions and current product behaviour; bundled references guide
the workflow. If live docs are unavailable, inspect existing configuration and available
dashboard values, say what remains unverified and defer edits that depend on an unknown
schema. Don't invent accepted settings or current product details.

## Deliver changes

Start with the outcome the user wants and the repository's instructions. Inspect the
parts of the code and tests needed to deliver it, then identify changes that can stand
alone and those that must be reviewed together. Preserve the user's scope and workflow.

Read the policy before you plan. Run `okae config show --brief` in the repo, or use the
summary a session-start hook already added. It names the size limits, protected paths
and the changes that always need human review. If the CLI isn't signed in or
the command fails, say so and continue without it.

Infer the team's PR style from the repo before choosing boundaries. Look at a handful of
recently merged PRs, for example with
`gh pr list --state merged --limit 20 --json number,title,additions,deletions,changedFiles`,
and any contribution guide. Match their usual size, scope and description style.

Choose PR boundaries for a coherent, safe solution. Keep implementation, tests and
other dependent changes together when they only make sense together. Each separately
assessed PR can use a credit, while eligible reassessments of the same PR are included.
Split only when it realistically saves review time, such as a routine piece Okae can
approve on its own while a person reviews the part that needs human review. Explain the
dependencies, order and extra credits when you propose a split. Each PR must work on its
own and give reviewers the evidence they need.

Never shape a change to get past review. Avoid these:

- Splitting work to get under size limits or out of a protected path.
- Staging dormant capability across PRs, such as code a later PR switches on.
- Separating changes that must deploy together, such as a migration and the code that
  depends on it.
- Opening an intermediate PR that breaks the build, tests or behaviour on its own.
- Weakening, skipping or deleting tests to make a change look routine.
- Changing `okae.yml` or settings to avoid review, or promising the user an approval.

Before you push or open a PR, commit and run `okae preflight`. It compares your commits with
the default branch and lists the rules that mean the PR will need human review, with the
matching files. It sends metadata only and uses no credits. If a rule matches, confirm
the change is intended. Keep it and tell the user up front that the PR will need human
review and why. Only drop a change the user didn't ask for that slipped in, such as a
stray lockfile update. A clean preflight means no rule matched. The assessment still
reviews the diff, so it doesn't promise approval.

Where relevant and available, check approval blockers in the dashboard and `okae.yml`
at the PR head. File values can override saved defaults, and the brief summary and preflight
read the default branch. If effective settings aren't available, say what remains
unknown; the published assessment determines the route for the actual PR.

For a concrete request, choose the suitable shape and proceed under the user's and
repository's permissions. Explain a multi-PR plan when it matters; don't turn a simple
task into a planning exercise. Keep PR titles and descriptions clear about the change,
its purpose, evidence and dependencies so reviewers can make an informed decision.

## Set up Okae

If the owner prefers the dashboard or you can't run commands on their machine,
send them to the [Okae dashboard](https://app.okae.ai) to sign in with GitHub.
The setup guide takes them from connecting a repo to their first PR assessment.
End the handoff there. If they return with a question, help with that step.

For terminal setup, follow the [CLI setup guide](references/installation.md).
Run `okae init` in the owner's repo, or pass `--repo OWNER/NAME` to select it.
If they want to connect a workspace before choosing a repo, run `okae login`
from any directory. The owner authorises access in a browser on the same machine.

During browser setup on either path, the organisation owner installs the Okae
GitHub App if needed and selects the repos it can access. For an existing
installation, update access only if the intended repo is missing, so check that
with the CLI and direct them to set it up if they haven't already.

When the owner wants help choosing checks, read the effective policy in the
dashboard or with `okae config show --json`. Follow the
[configuration workflow](references/configuration.md). Keep settings that fit.
Ask about consumers, sensitive paths and approval preferences the repo can't
tell you about.

Setup ends when the owner’s choices are effective. If a file change still needs to
land, identify it. Offer a real assessment separately. Let the owner select the PR
before starting a run that can spend a credit.

## Deliver and verify

When asked “Am I getting the most out of Okae?”, start with existing history.
If the owner wants a higher approval rate, look for recurring changes they consider routine
and would be comfortable delegating under a different rule setting.
Run `okae assessments list --json` in the checkout (or add `--repo OWNER/NAME`).
Use `--workspace` for a workspace-wide request. State which repos and how much
history you inspected. Page with `--limit` and `--offset` if the question needs it.

- Group by repository and PR number. Use the latest completed Approve or Review
  judgement per PR in the period. Compare earlier runs by head SHA to show which
  concerns changed. Report pending, skipped and failed runs separately, including
  when the newest revision still awaits a judgement.
- Use `approval_submitted` to count actual GitHub approvals. Identify shadow
  Approve results from `approval_mode`. Read every entry in a Review's `reasons`
  array. One PR can contribute to several reasons. A missing reason is unknown.
- Pick a few examples and show the owner the PR, assessed revision and recorded
  reasons. Inspect the diff at that revision when the reason alone is ambiguous.
  Ask which of those changes they would delegate and which they want to review.
  An overlapping reason can still require review if one setting changes.
- Read the current effective policy before proposing an adjustment. Keep a
  policy that matches the owner's choices. For an evidenced mismatch, follow
  the [configuration workflow](references/configuration.md) to preview one
  supported change. Historical results establish what happened under the
  policy at the time. Looking them up needs no new assessment or credit.

Treat the expected route as a prediction until Okae assesses the actual PR head. A small
PR may still need human review because of its content or assessment. An approval also
depends on effective settings and service gates; don't promise one or change policy to
obtain one. A shadow result isn't an approval and Okae doesn't merge PRs.

Inspect the published result and assessed version when available. If Okae requests human
review, explain the reason and leave the relevant work for review; don't edit unrelated
code to make the check green. For an error or missing assessment, use the troubleshooting
guidance in [installation and verification](references/installation.md). Follow the team's
branch protections and authorization for opening, updating and merging PRs.
