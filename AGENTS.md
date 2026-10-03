@PROJECT_CONTEXT.md

# Agent Guidelines & Standing Rules

## 🚨 MANDATORY HANDOFF PROTOCOL: `PROJECT_CONTEXT.md`
`PROJECT_CONTEXT.md` is the **single source of truth** for project context and handoffs between **Antigravity** and **Claude Code**.

1. **Session Start**:
   - If `PROJECT_CONTEXT.md` exists, read it in full before taking any action or writing code (auto-imported above if supported).

2. **Session End / Handoff**:
   - Before ending any session in which you changed code, config, dependencies, deployment, servers, secrets (names only), or project structure:
     1. Update affected sections of `PROJECT_CONTEXT.md` and their "Last verified: YYYY-MM-DD" dates.
     2. Rewrite the "Handoff notes" section: what was done, what is unfinished, and next steps.
     3. Add a dated one-line entry to the document's changelog (newest first).
     4. Check that the document contains no secret values (names only, never values).
     5. Include `PROJECT_CONTEXT.md` in the same commit as the change it describes.
   - If nothing relevant changed, leave `PROJECT_CONTEXT.md` untouched.
   - Never remove information unless it is confirmed obsolete.

---

## Development

When starting the dev server, use background mode:

```
astro dev --background
```

Manage the background server with `astro dev stop`, `astro dev status`, and `astro dev logs`.

## Documentation

Full documentation: https://docs.astro.build

Consult these guides before working on related tasks:

- [Adding pages, dynamic routes, or middleware](https://docs.astro.build/en/guides/routing/)
- [Working with Astro components](https://docs.astro.build/en/basics/astro-components/)
- [Using React, Vue, Svelte, or other framework components](https://docs.astro.build/en/guides/framework-components/)
- [Adding or managing content](https://docs.astro.build/en/guides/content-collections/)
- [Adding styles or using Tailwind](https://docs.astro.build/en/guides/styling/)
- [Supporting multiple languages](https://docs.astro.build/en/guides/internationalization/)

## 🚢 Deployment Procedure

This project (the Astro portal) is served by the `BackendAPI` Docker container running on the remote EliteDesk server (`100.98.28.34` / `192.168.10.168`). To deploy changes:

1. Build the Astro project locally:
   ```bash
   npm run build
   ```
2. Copy the static build output (`dist/`) into the `BackendAPI`'s `public/` folder, which is where the backend serves static files from:
   ```bash
   rsync -av dist/ /home/robcasagrande/Projects/SmartCheckInSuite/BackendAPI/public/
   ```
3. Run the deployment script from the `BackendAPI` directory to sync and rebuild the Docker containers on the remote server:
   ```bash
   cd /home/robcasagrande/Projects/SmartCheckInSuite/BackendAPI && ./deploy_elitedesk_backend.sh
   ```
This will push the new files via SSH, rebuild the `backend-api` container, and restart it so the changes take effect immediately on `http://192.168.10.168/`.

## ⚡ Working style (set by the owner, 2026-10-03)
- Work autonomously. Don't ask for confirmation on routine decisions (approach, naming, file layout, small refactors, dependencies, running builds/tests); pick the sensible default and note the assumption in your summary.
- Batch any open questions at the end of the work instead of stopping mid-task.
- Only stop and ask first before destructive or irreversible actions: deleting files, data, branches or repos; force-push or history rewrites; production deploys or restarts; touching live databases; changing secrets, servers, firewall or accounts.
- More specific rules elsewhere in this file take precedence over this section.
