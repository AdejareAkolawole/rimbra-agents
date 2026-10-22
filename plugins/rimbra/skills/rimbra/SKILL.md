---
name: rimbra
description: Deploy and manage apps on Rimbra (rimbra.app) — projects, deployments, build and runtime logs, rollback, settings, environment variables, databases and backups, domains, email and WhatsApp. Use when the user mentions Rimbra, a *.rimbra.app site, or wants to deploy, debug a failed deploy, roll back, or change variables or databases on Rimbra.
---

# Working with Rimbra

Rimbra hosts the user's apps. You reach it through the `rimbra` MCP server. If its tools aren't available, ask the user to run `/mcp` and sign in to Rimbra.

## The model

- A **project** is a site at `<name>.rimbra.app`, built from a GitHub repository. Every push to its production branch redeploys.
- Pushes to other branches build **previews** at `<name>-<branch>.rimbra.app` when previews are on.
- A monorepo deploys one folder per project: a frontend and a backend are two projects.
- **Environment variables** belong to a project and apply on the next deploy. Scopes: Production, Preview, Development.
- **Rollback** makes an older ready build live instantly, without rebuilding.
- **Databases**: Postgres, MySQL, Redis. Connecting one to a project adds `DATABASE_URL` (done in the dashboard).
- You can't pay for anything, buy domains, or change billing or the team. Send the user to https://app.rimbra.app for those.

## Deploy and check

1. `list_projects` to find the project's exact name.
2. `deploy_project` returns a deployment id.
3. Poll `get_deployment` every 20–30 seconds until the status is `ready` or `failed`. Builds take one to three minutes.
4. When it's ready, give the user the address.

## When a deploy fails

1. Read the last lines of `get_deployment`. They usually name the problem.
2. Missing environment variable: confirm the value with the user, `set_env_var`, then `deploy_project` again.
3. Wrong folder or commands: compare `get_project` settings with the repository (root directory, build and start commands). Fix the code or ask the user to change the setting in the dashboard.
4. The app builds but errors at runtime: `get_runtime_logs`.
5. The live site broke after a deploy: offer `rollback_project` to the previous ready build (ids come from `get_project`), then fix forward.

## Databases

- `create_database`, then `connect_database` to the project (adds DATABASE_URL), then `deploy_project`.
- `backup_database` before risky changes. `restore_backup` replaces the data (a safety backup is taken first); always confirm.

## Email and WhatsApp

- Email: `add_email_domain` with a from address, give the user the DNS records, wait until `list_email_domains` shows it verified, then `send_email`.
- WhatsApp: numbers are connected in the dashboard; `send_whatsapp` sends from one.

## Care

- Confirm with the user before `rollback_project`, `set_env_var` on Production, `create_project`, `create_database`, `restore_backup`, `send_email`, `send_whatsapp`, `contact_support`, or any `query_database` statement that changes data.
- Never print secret values back to the user. Variable values aren't returned by the tools anyway.
- Keep `query_database` reads small: add `LIMIT`.
