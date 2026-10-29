---
name: seflo-organize-work
description: Find, create, and organize Seflo tasks and projects when the user names a task, task code, project, or work to capture in Seflo. Use for requested local updates and checklists; solving the task itself and preparing an external reply are separate workflows.
---

# Organize work in Seflo

Use the connected Seflo MCP tools. Follow the user's requested scope and language.
An explicit request to create or update a record is sufficient direction to do
that work; do not add a conversational approval step for routine local writes.
Respect the client's tool permissions. Ask only for missing essential information
or an ambiguous target, not for internal IDs or optional fields.

## Resolve the target

- For a task code such as `S-123` or `PHX-4`, call `seflo_get_task` with the code.
  Use its returned immutable ID for tools whose schema requires a UUID.
- Resolve a project name or prefix with `seflo_list_projects`. Prefer an exact
  match; disambiguate multiple plausible matches. A requested destination must be
  active. Do not create a missing project just because a task names it.
- For a task title, use `seflo_list_tasks`, narrowing by a known project and any
  explicitly requested filters. There is no title-search parameter: compare
  returned titles and follow `next_cursor` with unchanged filters. Do not silently
  restrict a general title search to To Do; completed tasks can also match.
- If no current task matches, inspect source-archived history with
  `include_archived_tasks=true` and the separate manually archived collection via
  `seflo_list_archived_tasks`. Use the user's narrower scope when supplied.
  A partial listing is not proof of absence. If a listing cannot be completed,
  explain what was searched and ask for a project or task code to narrow it.
- Before changing a title-matched task, establish a unique match in the requested
  scope. Show codes, projects and titles to distinguish duplicates; do not guess
  from recency, a different conversation, or a phrase such as "that task" alone.

## Create and update

- For a new project, derive a short, meaningful prefix when omitted; check that
  it is available and meets the current tool schema. Preserve an explicit prefix.
  An existing same-name project is a possible match, not permission to duplicate it.
- For tasks, derive a concise title and description from the supplied work. Keep
  default priority/stage unless the user specifies otherwise; do not invent a
  deadline or project. Create in the resolved project in the initial call.
- For combined requests, create the requested project first and use its returned
  ID for the requested tasks. Report partial success instead of recreating records
  that already succeeded. Reuse the same idempotency key for an identical retry
  where the tool supports it; changed work requires a different key.
- Read the current record before a partial update and preserve unrequested fields.
  Local edits use `seflo_update_task`; source-owned changes require the currently
  offered action workflow. An internal comment is not an external reply.
- Use checklist tools when requested. Do not override an incomplete-checklist
  guard without the user's explicit instruction. Verify the returned stage before
  saying a task is Done.
- Move, archive, restore or delete only as requested. Moving projects permanently
  changes a task's human-readable code; use and report the returned new code.

Return a concise account of what was found or changed, with the returned task
code, project and available URL. Do not claim an unverified write or invent links.
