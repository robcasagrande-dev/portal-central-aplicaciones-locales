---
name: handoff
description: >-
  Hands the current task off to the next session (Antigravity or Claude Code):
  updates the PROJECT_CONTEXT.md handoff notes and changelog, commits and
  pushes the branch. Use when the user types /handoff, before stopping, or
  when the usage limit is close.
---

# Hand off

1. If this session changed code, config, dependencies, deployment, servers,
   secrets (names only) or project structure, update `PROJECT_CONTEXT.md`
   (create it with `## Overview`, `## Handoff notes` and `## Changelog` if it
   is missing):
   - the affected sections and their "Last verified: YYYY-MM-DD" dates;
   - rewrite "Handoff notes": what was done, what is unfinished, the branch,
     and clear next steps;
   - add a dated one-line changelog entry (newest first);
   - check the file holds no secret values (names only).
   If nothing relevant changed, leave it untouched. Never remove information
   unless it is confirmed obsolete.
2. Commit the work together with `PROJECT_CONTEXT.md` on the feature branch
   and push the branch (`git push -u origin <branch>`). Several sites deploy
   to production on every push to `main`/`master` (see `AGENTS.md`): merge or
   push there only with the owner's yes.
3. Finish with the branch name and the next step in one or two lines.
