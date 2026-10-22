# tkg-ops

Day to day operations content for TKG Group. Lives on this branch for now because this session is bound to this repo. Move or extract later as needed.

## What is here

1. `run-my-day.md`. The one prompt Jason paste runs each morning (and again later in the day as approvals come in). Chains the email scan, procurement, logistics, estimator, and books agents against new email and newly accepted estimates. Produces drafts only. Nothing sends or books without Jason's go.

2. `logistics-agent.md`. The skill definition for a new logistics agent (does not exist yet in Jason's Claude account). Two modes: quote (adds freight to an estimate) and dispatch (books the carrier). Knows all season road, winter road, and fly in lane rules for communities north of Pickle Lake. To actually install this as a skill, use the `skill-creator` skill in Claude and paste this file as the source, or add it under `~/.claude/skills/logistics-agent/SKILL.md` on your laptop.

## Assumptions baked in

- "Email agent" means the email scanning that `procurement-agent` already does for intake, plus `invoice-collector` for filing supplier invoices and receipts. If you have a separate email agent, swap the name in `run-my-day.md`.
- Existing user level skills being orchestrated: `procurement-agent`, `estimator-agent-2`, `invoice-collector`, `books-agent`, and (new) `logistics-agent`.
- Nothing external sends or books without Jason's approval. Everything lands in Outlook drafts or Square draft estimates.
- Jason's existing Square customer records and the master budget workbook structure described in his user skills are the source of truth.

## Caveats

- The logistics agent assumes current winter road behaviour that is roughly right for communities like Pikangikum and Wapekeka, but it needs a refresh each year at freeze up and at thaw. The dates shift.
- The carrier list (Wasaya, North Star Air, Perimeter for air; Manitoulin, Day and Ross for truck) is a starting point. Add or remove based on actual TKG lane experience.
- The estimator margin rule (75 percent markup under $10 landed cost, 30 percent otherwise) is copied from `estimator-agent-2`. If you change the rule there, update `run-my-day.md` to match.
