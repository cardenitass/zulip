# AI assistance — CoreX AV2

- Tool: OpenAI Codex, local workspace and connected GitHub read tools.
- Date: 2026-11-08 (America/Guatemala).
- Objective: implement the second-deliverable increment for Zulip #7719.
- Prompt reference: the team's task in this Codex conversation beginning
  “Implement the CoreX second-deliverable increment for Zulip issue #7719”,
  including CA1–CA5, architecture, evidence and publishing restrictions.
- Human review: the evidence below records local validation; it does not
  establish final human acceptance.

Validation continued on 2026-11-09 after the user reported Docker working.
The agent provisioned the official Linux CI image, executed backend and Node
tests, corrected a transaction regression, OpenAPI encoding, migration field
type, test cleanup and active-user detection, and added a Puppeteer integration
test. The 134-test backend run includes a real two-connection race. The complete
Node suite and migration consistency checks passed. Mermaid CLI rendered the
sequence. Browser integration exposed a keyboard-selection assertion. Source
inspection then identified the global Space hotkey intercepting banner buttons.
A localized handler and regression test preserve native activation of both
mention actions.

Commands and outcomes from the continuation are recorded in the resumed
validation section of the evidence document. An earlier Docker-dependent run
was blocked by a permission request; validation continued later.

On 2026-11-21, Codex helped validate the changes in a separate Docker checkout
at base `416dc8c483405fef2e687d811de1f57cf81c9372`, with the PR's migration
and browser test changes. The published and expanded Puppeteer tests passed.
The expanded test checked Notify and Subscribe flows, the recipient's link to
the original message, and a known passage in the quote. The migration conflict
was resolved with a no-op merge, then checked on a fresh database and from a
state where the CoreX migration had already been applied. `./tools/test-migrations`
passed. The provisioning script recreated the container's shared development
databases. See the follow-up section of the evidence document for details and
the limits of those results.

Affected areas: compose warning templates and validation/setup/send/recipient
lifecycle; local echo and transmit request types; send endpoint; new internal
notification action; unique delivery model and migration; backend and web tests;
OpenAPI and generated unmerged API changelog; help article; architecture and
evidence documentation. See the scoped diff for the exact file list.

Decisions requiring human validation: synchronous atomic delivery and its
latency; silently skipping newly ineligible recipients; current private-channel
join/access semantics; rollback of the original on unexpected DM failure;
database race-test correctness; no subscriptions changed; accessibility and
composer lifecycle, including retries and scheduled-message exclusion.

Commands and actual results, baseline, environment, test blockers, metrics,
traceability and the Spanish PDF handoff are recorded in
[docs/evidence/av2.md](evidence/av2.md). Source inspection used `rg`, `Get-Content`,
Git status/log/diff/remotes and file inventory. Static checking used Python Ruff
on the six affected Python files. Repository tests and lint were attempted using
the actual scripts and failed before collection on Windows. The generated API
changelog helper ran; its automatic Git staging failed. No dependencies or
provision checks were bypassed. No credentials or private test data are included.

No AI-generated messages were sent to Zulip development chat during the
documented development. The team must read, understand and test this work per
Zulip's AI use policy.
