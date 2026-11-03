# Configure repository policy

Fetch the [configuration guide](https://docs.okae.ai/docs/configuration) before creating,
changing or explaining settings. It owns supported keys, accepted values, defaults,
limits, precedence and approval behaviour. Use the dashboard for the repository's actual
effective settings and their sources. Read [Safety and limits](https://docs.okae.ai/docs/safety)
when explaining assessment guarantees or recommending policy changes.

## Choose an approach

Inspect repository instructions, review policies and existing configuration. Help the
user choose between using valid defaults, editing saved repository defaults or maintaining
an optional `okae.yml` with their code. Recommend the smallest change that meets their
needs. Preserve existing choices and explain uncertain policy decisions before editing.

When a file is chosen, propose only agreed overrides and use sensitive paths that actually
exist. Avoid copying a complete defaults snapshot. Show the diff and follow the repository's
branch and review process. Check syntax and documented keys, types and ranges with
available tooling. Static validation doesn't prove that Okae assessed the changes.

Use the configuration guide's applying-changes and approval-mode guidance, then verify
the intended PR's real result and GitHub review state. Preserve the team's branch protections.

## If the docs are unavailable

You can inspect existing configuration and available dashboard values, explain what you
observed and identify choices to discuss. State what remains unverified. Defer policy edits
that require an unknown schema or current behaviour; don't infer accepted settings from
an example or remembered values.
