---
name: explain-back
description: Re explain the most recent technical action in plain non technical language. Trigger when Jason says "what did you just do", "explain that to me", "in plain English", "I don't follow", or similar.
origin: tkg-platform
---

# Explain Back

Translate the most recent technical action into language Jason can actually use.

## When to use

- Jason asks "what did you just do" or "explain that to me".
- Jason asks "in plain English" or "I don't follow".
- A long stretch of tool calls just happened and Jason has not seen anything explained yet.
- After any database migration, RLS policy change, deployment, or config edit.

## How it works

1. **Read `memory/jason-context.md`** to refresh tone rules. No dashes in prose. Plain language first.
2. **Identify the most recent meaningful action.** A "meaningful action" is one that changed state somewhere (committed code, ran a migration, deployed, edited a config, created a Supabase resource). Skip pure reads.
3. **Answer four questions, in this order, in two or three sentences each.** Use line breaks, not headers, unless the action was large.

   - **What happened.** What did I actually do, in nouns and verbs Jason would use.
   - **Why it mattered.** What problem this solved or what capability this unlocked.
   - **What changed.** What is different now versus before. Mention specific files, URLs, or screens Jason can look at.
   - **What is next.** One recommended next step.

4. **No code dumps.** A line of SQL or a function name is fine if it is the thing being explained. A full file is not.
5. **Stop.** Do not chain into another action. Wait for Jason.

## Tone examples

Bad: "I ran a CREATE POLICY statement on the patients table to enforce per role row level security."

Good:

> I added a rule to the patients table so that only admins and coordinators can see patient rows. Finance and viewer roles get nothing back, even if they query the table directly.
>
> Why it mattered: before this, anyone with a login could read every patient. That would have failed a PHIPA review.
>
> What changed: the patients table in Supabase now has a policy attached. You can see it in the Supabase dashboard under Authentication, Policies.
>
> Next: I would test it by logging in as a viewer account and confirming the page is empty.

## Guardrails

- Never use the explanation as a way to ask Jason to make a technical choice. If a decision is needed, recommend one and say why.
- If the action was actually small and Jason just missed it, say that. Do not pad.
