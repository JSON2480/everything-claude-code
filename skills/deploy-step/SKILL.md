---
name: deploy-step
description: Execute one deployment step from README.md at a time, verify it worked, update project state, and check in with Jason before moving on. Use for any "deploy", "set up Supabase", "set up Vercel", "wire auth", or README walkthrough request.
origin: tkg-platform
---

# Deploy Step

A discipline for walking through `README.md` deployment instructions one step at a time with Jason (TKG NIHB Platform).

## When to use

- Jason asks to start, resume, or continue deployment.
- Jason references a README section by number ("do step 2").
- A previous session ended mid step and we are picking it up.

## How it works

1. **Load context.** Read `memory/project-state.md` and `memory/jason-context.md` first. Then read the specific README section requested.
2. **Restate what we are about to do** in one or two plain sentences. No dashes in prose.
3. **Do the work.** Execute the commands or edits the README specifies. One step only. A "step" is one of the five top level README steps, not a sub bullet.
4. **Verify.** Run the verification the README defines (a command, a curl, a page load). Capture the output.
5. **Update `memory/project-state.md`.** Fill in identifiers (Supabase project URL, repo URL, Vercel URL, etc.), move features between sections, log any issue hit.
6. **Tell Jason what happened in plain language.** What did we do, what changed, what is next. Reference any identifier we now have.
7. **Stop.** Ask Jason to confirm before starting the next major step. Never chain two major steps without a check in.

## Guardrails

- Never run more than one major README step per invocation.
- Never commit secrets. If a value is sensitive (API key, service role key, DB password), tell Jason where to paste it himself (Supabase dashboard, Vercel env vars) and do not write it into any file.
- If a verification fails, stop. Diagnose. Update `memory/project-state.md` Watch List. Do not paper over the failure to keep moving.
- If the README is ambiguous, ask Jason a single concrete question with a recommended answer.

## Example shape

```
[Reading project state and README Step 1]
About to create the Supabase project in Canada Central, on the free tier.

[Walks Jason through the dashboard clicks, or runs the CLI if applicable]

Verified: dashboard shows the project as ACTIVE in ca-central-1.
Updated memory/project-state.md with the project ref.

Next step would be the database schema (README Step 2).
Want me to start that, or pause here?
```
