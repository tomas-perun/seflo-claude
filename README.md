# Seflo for Claude

![Seflo](assets/icon.png)

Turn conversations into organized work in your personal Seflo workspace.
Seflo connects Claude to your tasks, projects, Knowledge and supported source
context. Five included skills guide common workflows while the remote MCP
server enforces account access and action permissions.

**Directory status:** prepared for review; not yet submitted or published.
This repository is the distribution package, not a public-directory install link.

## Connect

An authorized Seflo account is required. Connected-source workflows additionally
require that source to be connected in Seflo and the relevant permissions.
Account availability and service terms are described at https://seflo.ai.

For a preview, add a custom connector in Claude using https://app.seflo.ai/mcp,
then sign in to your own Seflo account and review the OAuth consent. The scope is
`seflo.tasks`. Do not paste passwords, tokens or API keys into a conversation.
Custom connector availability and organization approval depend on your Claude plan.

Once the plugin is available in the directory, add it and open its Connectors tab
to connect Seflo. The plugin references the same server as the standalone Seflo
connector; use that connection rather than adding duplicate copies. Organization
administrators may need to enable it before members can connect their accounts.

## Included skills

| Skill | Example request |
| --- | --- |
| Organize work | Create a task in project Winter launch, or find Prepare launch notes by title. |
| Manage Knowledge | Save these decisions as a Knowledge article in Winter launch. |
| Resolve task | Read S-123 and its attachments, prepare the solution and show the reply for review. |
| Daily brief | What should I work on next in Winter launch? Do not change anything. |
| Communication catch-up | Review the available recent messages and suggest actionable follow-ups. |

Use task codes such as S-123, project names or task titles. Internal identifiers
are resolved by the tools. Ambiguous titles need clarification. Skill instructions
guide Claude; they do not replace server-side permissions or guarantee its output.

## Review external actions

Seflo can prepare supported replies and handoffs with attachments. Preparation
does not send a message. Review the destination, content, files and effects in
the Seflo action panel before confirming execution. If the embedded panel is
unavailable, open the authenticated Seflo web fallback. An uncertain result must
be checked on the existing action, not retried as a new send.

Native task, project and Knowledge updates are separate from external actions.
Changing a local task does not imply that a source message was sent. Available
actions depend on the source and permissions. Communication catch-up reports its
actual source coverage; unavailable sources are not evidence of an empty inbox.

## Reviewer walkthrough and App examples

[Watch the reviewer walkthrough](https://youtu.be/c6vq83100Jk) (4:05, English
narration and captions). The video uses edited captures from the dedicated
synthetic workspace and shows all five skills, attachment preparation, the
interactive review panel, and independently verified delivery. It is not a
continuous recording. Reviewer credentials are supplied privately, not here.

The following PNGs are actual Claude App responses, cropped to the App and at
least 1000 pixels wide. They contain synthetic demo data only.

| App response | Prompt and interaction |
| --- | --- |
| [Review a prepared reply](assets/reviewer-app/review.png) | "Resolve CRV-4: read its source context and original launch-costs.csv, calculate Revenue minus Expenses, prepare a completed CSV and a concise reply, and show the Seflo review panel. Do not send yet." |
| [Choose files](assets/reviewer-app/files.png) | Continue the same prepared reply, then open **Reuse files** in the App to inspect available files. Preparation and file selection do not send the reply. |
| [Completed action](assets/reviewer-app/completed.png) | Review the destination, edit the reply, inspect the selected completed CSV, then explicitly click **Send and complete**. The completed response confirms the recorded action result. |

CRV-4 is the completed demonstration in the video and screenshots. For a fresh
review, use the open **CRV-5** budget email task and the private test instructions.
Its destination is email, so its available controls differ from the demonstrated
Trello comment. Never send again merely to reproduce a completed screenshot.

## Data and permissions

This package contains Markdown workflow instructions and JSON configuration. It
runs no local server, hooks, shell commands or background process and installs no
runtime dependencies. The MCP connection sends authorized requests to
https://app.seflo.ai/mcp. Seflo returns requested workspace data, which can include
tasks, Knowledge, source context and attachment contents, to Claude. Confirmed
external actions may deliver content and files to the selected connected service.

Only connect accounts and disclose information that you are authorized to use
with Claude. Do not use the integration for prohibited or restricted data. Claude
processes returned content under its own terms and your account settings. You can
disconnect Seflo or revoke the connection. No credentials are bundled here.

- [Privacy policy](https://seflo.ai/privacy)
- [Terms of service](https://seflo.ai/terms)
- [Support](https://seflo.ai/support): support@seflo.ai

## License and attribution

The instructions and package metadata use the MIT license in LICENSE. Seflo's
name and logo remain reserved; this license does not grant trademark rights.
The hosted service and application source are not included. Seflo is provided by
Tomáš Lysek and is not made or endorsed by Anthropic.
