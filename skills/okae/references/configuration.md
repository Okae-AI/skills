# Recommend a repository policy

Read the live default-branch settings with `okae config show --live --json`,
or open the repository's Settings tab. In a checkout, `okae config show --json`
previews the local root `okae.yml`. Check each field's value, source and
constraints, and any configuration errors before suggesting a change.

Start with the repository's purpose and existing review rules. Check manifests, public
entry points, deployment files and ownership rules. A library with downstream consumers
may need compatibility checks; an application can also expose an API even when its
package has no exports. Ask who depends on the interface before suggesting a change.
For a protected path, show the exact proposed pattern, examples of real files
it covers, and any nearby files it leaves outside. Keep all existing protections
when adding a pattern to the list.

Keep defaults that fit. For a managed field, use the current
`storage.repository.revision` as the draft's `expected_revision`. Preview with
`okae config preview --file changes.json`, show the effective differences and save
the agreed draft with `okae config apply --file changes.json --yes`. Read the live
result back. If the revision changed, refresh, rebase the draft on current values
and preview again. Explain the effect of enabling GitHub approvals.

If a file overrides the field or is invalid, fix the reported key in the root
`okae.yml` and preview the patch with `okae config preview --json`. From outside
the repo pass `--repo OWNER/NAME --file /path/to/your-repo/okae.yml`. Show the
before/after values and sources. A valid preview can have no effective changes.
File edits take effect on the revision containing them. For a past assessment,
inspect `okae.yml` at its recorded `target.head_sha` and the published check
when available. Today's defaults alone can't verify historical managed settings.

Use the [configuration reference](https://docs.okae.ai/docs/configuration) for supported
keys and precedence. `strictness` sets every signal's level. To delegate one recurring
reason, adjust that signal under `signals` rather than the whole preset. Don't recommend
turning off a security signal.
