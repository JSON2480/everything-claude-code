---
name: build-feature
description: Add a new feature to the TKG NIHB Platform after it is deployed. Follows existing patterns. Use when Jason asks to build, add, implement, or wire up any new capability on top of the deployed platform.
origin: tkg-platform
---

# Build Feature

Add capability without reinventing structure. Match the patterns already in the repo.

## When to use

- Jason describes a new screen, table, report, or workflow.
- Jason asks to "add" or "wire up" something on the live platform.
- A request that is not part of the README deployment path.

## How it works

1. **Read context first.**
   - `memory/project-state.md` (what is already deployed)
   - `memory/jason-context.md` (tone, constraints, communication rules)
   - `memory/decisions.md` (so we do not contradict an earlier decision)
   - `tkg_platform_spec.md` if present in the repo root
   - `tkg_design_system.md` if present in the repo root

2. **Find the closest existing pattern.** Grep the codebase for a screen, table, or query that already does something similar. Mirror its file layout, naming, and component shape.

3. **Plan in plain language and confirm.** Tell Jason what you intend to add, where the files will live, and which existing patterns you are mirroring. Recommend one approach. Stop and confirm before writing code unless the change is genuinely trivial (a label change, a copy edit).

4. **Implement.**
   - Use TypeScript and React conventions already in the project.
   - Use the design tokens from `tkg_design_system.md`. Do not introduce new colors or fonts.
   - Use existing Supabase client wrappers. Do not open a new client.
   - If the feature touches patient data, add or extend an RLS policy. Never bypass RLS with the service role from the browser.
   - If the feature changes data, add an entry to the audit log.

5. **Verify locally.**
   - Run typecheck. Fix any error before continuing.
   - Run lint. Fix any error before continuing.
   - If a dev server is available, exercise the feature in the browser. Test the happy path and at least one failure case (no permission, empty data).

6. **Commit.** Conventional commit message. One feature per commit when possible. Example: `feat(claims): add per community claim summary view`.

7. **Update `memory/project-state.md`.** Move the feature from pending to complete, or add it to complete if it was unscheduled. Note any new identifier (new table, new route).

8. **Tell Jason what shipped.** Plain language. Use the `explain-back` skill style if the change was technical.

## Guardrails

- Never invent a new pattern when an existing one works.
- Never add a dependency without telling Jason what it does and what it costs (bundle size, license, maintenance burden).
- Never weaken RLS to make a feature work. If RLS is in the way, the feature design is wrong.
- Never write to the audit log table directly with UPDATE or DELETE. Append only.
- Never put secrets in committed files. Use Vercel env vars and `import.meta.env`.
- If a feature would push the platform off the free tier or break a PHIPA defensible posture, stop and surface that to Jason before writing code.
