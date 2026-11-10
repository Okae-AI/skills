# Set up Okae in your repo

Use a trusted installed CLI when available. If the user prefers a global install, follow the CLI reference below. If they prefer to skip installation, run it on demand with npx. Use Node.js 24 or
newer and a trusted npm executable. Run this from your home directory:

```sh
npx @okae/cli init --repo OWNER/NAME
```

Use your trusted npm registry. If the registry or @okae scope is remapped, verify the source before running the package. Reuse the same npx prefix and directory for subsequent commands. For a global
install or command flags, use [the CLI reference](https://docs.okae.ai/docs/cli).
If the owner prefers the dashboard, use [manual setup](https://docs.okae.ai/docs/manual).

Hand the browser to the authorised organisation owner for sign-in, agreement acceptance,
GitHub App permissions and CLI consent. Never ask them to paste tokens into chat.
After they return, read the current repo status and effective settings. When they started
in the dashboard, reuse their repo and branch selection and any existing settings.

When the owner wants to try an assessment, use available GitHub tools or run
`okae assessments run --json` without a target to list open PRs. Distinguish an empty
list from a failed request. Run the chosen PR once and report its assessed revision and
result. After an interrupted wait, inspect the accepted ID. For a missing or failed
assessment follow [troubleshooting](https://docs.okae.ai/docs/troubleshooting).
