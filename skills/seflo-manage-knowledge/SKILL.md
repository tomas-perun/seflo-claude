---
name: seflo-manage-knowledge
description: Find, create, or update Seflo Knowledge articles, including requests to save a conversation as KB, write a project document, or use a Knowledge template. Use when the requested output is a Seflo article, not a task or an external message.
---

# Manage Seflo knowledge

Treat "KB" as a Knowledge article. Use the user's language for the article and
response. Save or update when the user explicitly requests it; do not require
another approval for routine local writes. If the user only asks for a draft in
chat or a summary, do not save it without that instruction.

## Find the article and project

- Resolve a named project with `seflo_list_projects`; distinguish similar names
  and require an active project for new assignments. Do not silently create a
  missing project or assign content to a different one.
- Use `seflo_list_articles` with `search` and the project filter when known.
  Search covers titles and Markdown content. Follow returned cursors with the
  same filters; disclose a partial search. An article can also be unassigned or
  belong to an archived project, so do not silently exclude those from a global
  search. An update request does not authorize creating a missing article.
- Read the selected article with `seflo_get_article` before summarizing or editing
  it. If multiple articles match, ask using their titles and project context.
  Do not merge or overwrite articles merely because they share a title.

## Write useful content

- Derive a specific title from the supplied material when omitted. Write concise
  Markdown that preserves the user's facts, decisions, open questions and links.
  Do not invent missing facts to fill a template. Ask when the actual subject or
  required source material is missing.
- Use `seflo_create_article` with direct Markdown for normal content. Use a blank
  article, built-in PRD, or a personal template only when that starting point fits
  the request. Discover available templates with `seflo_list_article_templates`
  and inspect the chosen one with `seflo_get_article_template`; do not guess IDs.
- Assign the project during creation. For updates, preserve unrelated sections
  and existing project assignment; omit assignment fields unless moving the
  article was requested. Explicit null means No project, not "leave unchanged".
- Use supported idempotency keys for retries of the same creation. Inspect an
  uncertain result before repeating a write. Do not create extra tasks, templates
  or project documents beyond the requested scope.

Confirm the saved title and project, summarize material changes and provide the
returned URL. If only a draft was requested, clearly label it as unsaved.
