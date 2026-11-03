# Hosted setup and verification

Use the [manual setup guide](https://docs.okae.ai/docs/manual) for the current hosted
steps and [troubleshooting](https://docs.okae.ai/docs/troubleshooting) for recovery.
The quickstart at `/docs` installs this skill; once it's loaded, continue with hosted
setup rather than sending the user back through skill installation.

## Connect the organisation

Guide the user to [app.okae.ai](https://app.okae.ai). They need a GitHub organisation
owner account; personal-account repositories aren't supported.

An authorised owner signs in with GitHub, chooses the organisation, supplies its legal
business name and reviews the linked terms, DPA, subprocessor list and privacy notice.
The owner accepts on the organisation's behalf. Don't accept for them or promise data
handling beyond those documents.

Follow the hosted flow to install or connect the Okae GitHub App. In GitHub, select
**Only select repositories**, choose the intended repositories and review the displayed
permissions. Shadow mode doesn't reduce the App's granted permissions. Return to Okae
to complete the connection. Installing the App alone doesn't establish processing readiness.

If the App is already installed, check repository access and complete the existing
connection. The direct [App installation link](https://github.com/apps/okae-ai/installations/new)
is an alternative entry point; the owner still completes hosted setup and acceptance.

## Choose policy and check readiness

In **Getting started**, select the repository. Use valid existing defaults, edit saved
repository defaults or prepare an optional reviewed `okae.yml`. A new file isn't required.
Check the effective approval setting and its source; start new setups with approvals off.
Preserve existing human-review requirements and branch protections.

Check repository access, valid effective settings, active service and available credits
in the dashboard. Use [Credits](https://docs.okae.ai/docs/credits) for current charging
and purchasing guidance. Don't invent a balance or repeat the starter offer throughout
setup. You can finish later and resume the hosted guide.

## Verify a real assessment

Choose a suitable PR in the hosted guide, open an agreed PR or push an agreed change to
an existing PR. These repository actions still follow the user's permissions and workflow.
The configuration PR itself can be assessed and should require human review.

Check the **Assess changes** result on GitHub against the intended PR and assessed head
commit. Inspect its details and confirm the dashboard records the assessment. A sample
shown during setup, installed skill, generated YAML or successful installation isn't
evidence of a completed assessment.

In shadow mode, verify the notice and absence of a newly submitted Okae approval. An
Approve assessment and a submitted GitHub approval are separate facts. A Review result
is a completed assessment with a reason for human attention. An error isn't successful
verification. If you can't inspect the result, state what's unverified and guide the user
to check it rather than claiming completion.

Enable PR approvals later only when the team requests it and service approval access
allows it. Keep existing branch protections. Check actual GitHub reviews separately
from assessment labels. Okae doesn't merge or inspect branch rules.

## Recovery

| Symptom | Next step |
| --- | --- |
| Organisation unavailable | Check that the signed-in user is an organisation owner and the organisation installation is accessible. |
| Repository missing | Check the App's repository selection, then refresh the connection in Okae. |
| Agreement required | Return to hosted setup for an authorised owner to review and accept. |
| Credits required | Open the dashboard's Credits page, then rerun the blocked check after the balance updates. Adding credits doesn't retry it automatically. |
| Invalid configuration | Check `okae.yml` at the assessed head commit against the configuration docs. |
| No check or a processing error | Use the troubleshooting guide; collect the PR URL, assessed revision, time and any error ID for support. |

Don't change unrelated code or weaken policy to obtain an Approve result. Record
disagreements against the assessed revision. Anonymous feedback is an opinion, not
verified correctness evidence. An authorised owner can suspend or uninstall the App
through GitHub to stop processing.
