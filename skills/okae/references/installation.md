# Installation and shadow-pilot verification

## Before installing

Confirm with the service operator that the intended repository is approved for the pilot,
hosting is ready and the intended approval mode is agreed. Start with
`enable_approvals: false` unless the team explicitly requests PR approvals. Agree how private repository data is handled
before processing it. A public App can be installed outside the pilot, but installation
alone doesn't grant access to Okae's service.

Okae reads PR titles, descriptions, diffs and Git metadata. When rules don't decide the
route, the service sends PR evidence to TypeSafe's Jev API. Don't promise provider
retention, training exclusions or a storage region without the operator's confirmed terms.

## GitHub App

The authorised installer opens:

https://github.com/apps/okae-ai/installations/new

Choose the intended GitHub organisation, then **Only select repositories** and the agreed
pilot repository. An organisation owner completes workspace setup. Personal accounts aren't supported.

Review the permissions GitHub currently displays, including organisation Members read access
for owner verification. Shadow mode doesn't reduce the App's granted permissions.

If installed already, use the account or organisation's installed GitHub Apps settings
to check the repository selection. No individual Okae seats are needed for PR authors.

## Verify the trial

In the dashboard, select the repository and use valid defaults, saved repository settings
or a reviewed `okae.yml`. Confirm the available credit balance and readiness. Open an agreed
small PR or push to an existing open PR. Confirm:

- The **Assess changes** check and Okae comment appear on the assessed PR version.
- The shadow-mode notice appears and Okae submits no approval review.
- A green check means it would approve. A neutral result means human review or a processing
  issue to inspect in the details. Config edits should request human review.
- Existing human reviews and branch protections remain in place. Keep Okae's check
  optional during the pilot.

For an explicitly approval-enabled demo, review the effective `enable_approvals` setting
and blockers in the dashboard and confirm the operator has `APPROVE_PRS=true`. A routine result should receive
an actual approval review; verify that review separately from the green check. If either
switch is off, expect shadow mode instead.

Don't change branch rules or enable automatic approvals as part of ordinary pilot setup.
Only claim the checks you actually observed.

## Troubleshooting

| Symptom | Next check |
|---|---|
| No Okae check | Confirm installation, selected repo and supported PR event; give the operator the PR URL and time to inspect webhook delivery |
| Okae access required | Ask the operator to confirm repository-owner access. Changing the PR author won't fix it |
| Invalid okae.yml | Check the assessed head commit's config against the configuration reference |
| Couldn't check this PR | Send the operator the PR URL, assessed version, time and error ID |
| Config seems ignored | Confirm the filename and assessed head commit; explicit file settings override saved defaults |

Record feedback as `PR link | Okae result | Team's judgment | Reason`, preserving which
version was assessed when needed. Human approval alone doesn't establish that review was
unnecessary. An authorised person can suspend or uninstall the App to stop the trial.
