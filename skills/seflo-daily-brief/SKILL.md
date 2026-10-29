---
name: seflo-daily-brief
description: Review existing Seflo tasks to recommend today's priorities, the next task, or a project's current workload and evidenced blockers. Use for a read-only work briefing; scanning new messages and changing task priorities are separate requests.
---

# Review your Seflo priorities

Produce a short, evidence-based briefing in the user's language. This workflow
reads existing work; it does not change priorities, stages, projects or schedules.
Do not automatically scan communications or create tasks.

1. Honor a named project or time horizon. Resolve project names with
   `seflo_list_projects`; clarify ambiguous matches. For "today", use a known user
   timezone/current date; ask if unavailable and it changes the answer.
2. Read the relevant queue with `seflo_list_tasks`, following returned cursors and
   using current stage definitions when needed. Include actionable in-progress
   and waiting work as well as To Do; distinguish completed and archived work.
3. Inspect context for the most relevant tasks, rather than fetching every task's
   full context. Use actual deadlines, stated priority, current stage and explicit
   dependencies/blockers. Waiting alone does not prove a blocker, and no deadline
   does not mean low importance. Do not invent effort estimates or commitments.
4. Recommend up to three priorities, each with its task code, available link and
   a short reason. Use explicit user priorities first, then real overdue/near-term
   commitments and stated task priorities. Identify one practical next step.
   If the user asks about blockers, distinguish documented blockers from unknowns.
5. State relevant coverage limits: a partial listing, inaccessible project or
   missing information is not a complete workspace assessment. If no actionable
   work is found, say what was checked instead of inventing a recommendation.

Keep recommendations distinct from changes. Only execute a subsequent requested
mutation under that request's scope and the applicable Seflo tool permissions.
