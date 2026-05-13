# TKG NIHB Platform — Project State

> Living document. Update after every significant deployment task, schema change, or feature ship.
> Owner: Jason Dallaire. Maintainer when working in Claude Code: the active agent.

## Current Status

**Phase**: Pre deployment. Memory and skills scaffolding being set up.
**Live URL**: Not yet deployed.
**Last updated**: 2026 05 13

## Identifiers (no secrets — names only)

| Resource | Identifier | Notes |
|---|---|---|
| Supabase project URL | (pending) | Canada Central region required for PHIPA |
| Supabase project ref | (pending) | |
| GitHub repo | (pending) | |
| Vercel project | (pending) | Free tier to start |
| Vercel production URL | (pending) | |
| Custom domain | (pending) | |

## Roles in the system

- admin
- coordinator
- finance
- viewer

## Features

### Complete

(none yet — this is fresh setup)

### In progress

- Project memory and skills scaffolding (this branch)

### Pending

- Supabase project creation (README Step 1)
- Database schema and RLS policies (README Step 2)
- React app deployment to Vercel (README Step 3)
- Auth wiring and role enforcement (README Step 4)
- Audit log immutability checks (README Step 5)

## Known Issues / Watch List

- None yet recorded.

## Budget Snapshot

- Target: under $50 / month for first year.
- Users in first year: 2 to 5.
- Hosting: free tier where possible.

## Update Protocol

After every meaningful task:

1. Move features between sections (pending → in progress → complete).
2. Fill in identifier rows when resources are created.
3. Log any new known issue under Watch List with a date.
4. Bump "Last updated" at the top.
