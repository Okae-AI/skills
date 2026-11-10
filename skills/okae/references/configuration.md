# Recommend a repository policy

Read effective values, sources and the current revision with `okae config show --json`
or in dashboard settings. Use the [configuration reference](https://docs.okae.ai/docs/configuration)
for supported keys, precedence and limits.

Start with the repository's purpose and existing review rules. Check manifests, public
entry points, deployment files and ownership rules. A library with downstream consumers
may need compatibility checks; an application can also expose an API even when its
package has no exports. Ask who depends on the interface before suggesting a change.
For a protected path, point to a real file and explain who should review changes there.

Keep defaults that fit. Preview agreed managed overrides with
`okae config preview --file changes.json`, show the effective differences, and save
the approved draft using `okae config apply`. Read the result back. If the revision
changed, re-read current settings and review the new diff. Explain the effect of enabling
GitHub approvals and obtain the owner's explicit choice.

Offer an `okae.yml` diff for file-controlled fields or when the team wants policy in Git.
Before committing, run `okae config preview` in the checkout. From the temporary npx directory, pass `--repo OWNER/NAME --file /path/to/checkout/okae.yml`. Preserve unrelated policy and follow the repo's review process. Report which changes
are already effective and which still need to land on the relevant revision.
