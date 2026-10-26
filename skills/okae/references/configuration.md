# Repository configuration

Okae reads **`okae.yml` at the repository root** from each assessed PR head commit.
Settings layer service defaults, saved repository defaults and explicit file values in
that order. A missing file inherits defaults; invalid config requests human review.
Changing `okae.yml` itself requires review. The dashboard previews the default branch.

## Defaults and supported settings

```yaml
enable_approvals: false
assess_drafts: false
max_changed_lines: 500
max_files: 10
strictness: standard
protected_paths: []
extra_checks: []
```

| Setting | Accepted values | Default | Effect |
|---|---|---|---|
| `enable_approvals` | Boolean | `false` | Opts into PR approvals; also requires the operator's global `APPROVE_PRS=true` switch |
| `assess_drafts` | Boolean | `false` | Assesses draft PRs before they are ready for review |
| `max_changed_lines` | Integer 1 to 1500 | `500` | Larger PRs go to review without a model call. Counts additions plus deletions across the PR |
| `max_files` | Integer 1 to 10 | `10` | PRs with more changed files go to review without a model call |
| `strictness` | `standard`, `high`, `highest` | `standard` | Model concerns request review at 50%, 40% or 30%, respectively |
| `protected_paths` | List of nonempty repository-relative globs | `[]` | Any matching changed path, including its previous name, requests review |
| `extra_checks` | List containing only supported check names | `[]` | Adds optional model checks. Only `missing_tests` is currently supported |
| `unsafe_keep_stale_approvals` | Boolean | `false` | Disables Okae's withdrawal of its own stale approvals. Leave omitted or false during setup |

Numeric limits must be integers, not booleans or decimals. Strictness changes the model
cutoff; it doesn't disable rules or change size limits. Unknown keys are invalid.

Line and file limits don't enforce a token budget: line lengths, PR descriptions and diff
context vary. Larger limits also extend beyond the sizes measured in early benchmarks.

`missing_tests` asks whether a behaviour change lacks a test. This optional quality check
hasn't been benchmarked for safety. Enable it when the team requests that check.

## Protected paths

Paths are relative to the repository root. They must not start with `/` or contain a
`..` path segment. Matching is case-sensitive. `*` matches within a path segment; `**`
matches zero or more segments. Quote globs in YAML, especially those starting with `*`.

For a repository with payment and permission code in these directories:

```yaml
protected_paths:
  - "src/payments/**"
  - "src/auth/permissions/**"
```

Use paths actually present in the target repository. Describe why they need human review.
Paths supplement built-in protections; they don't replace or disable them.

## Mandatory rules and model questions

The service routes deleted or renamed files, protected paths and Git metadata such as
binaries, executable bits, symlinks and submodules to review. Built-in path rules cover
CI, manifests, lockfiles, licences, ownership, infrastructure, API schemas and migrations.

The model evaluates concerns about external behaviour, data integrity and access,
permissions, production configuration, third-party dependencies or services, and changes
harder to reverse than a code revert, plus an outside-rubric concern. Repository config
doesn't replace these questions or add arbitrary prompts.

Credentials, account access, the global approval kill switch, model selection and billing aren't supported
repository settings. Don't invent keys for them.

Set `enable_approvals: true` only when the team requests automatic PR approvals.
An effective false value keeps the repository in shadow mode. An omitted file value inherits
saved repository or service defaults, so check the effective setting and its source. The service switch can always
prevent approvals. Neither setting automatically revokes approvals already posted.

## Applying a config change

Have the team review and merge the config before relying on it for later PRs. The config PR
uses its own head-commit file and requires human review. Don't claim a static YAML check
simulates a live routing result.

Outside shadow mode, Okae normally withdraws its own earlier approval when a new result
requires human review, unless GitHub rulesets already prevent stale approvals counting.
The unsafe override can leave an old approval valid for newer changes. Prefer appropriate
branch rules over enabling it; the router currently checks rulesets, not classic branch
protection settings.
