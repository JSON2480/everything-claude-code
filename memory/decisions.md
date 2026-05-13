# TKG NIHB Platform (Decisions Log)

> One entry per architectural or product decision. Append, never overwrite.
> Format per entry: Date, Decision, Why, Rejected alternatives.

## 2026 05 13. Stack: Supabase + React + Vercel

**Decision**: Build the platform on Supabase (Postgres, Auth, RLS, Storage) with a React front end, hosted on Vercel.

**Why**:

- We own the data and the code. We can take a database export with us if we ever migrate off.
- Postgres RLS gives row level access control that we can audit. PHIPA defensibility benefits from explicit policies.
- Free tier hosting on both Supabase and Vercel keeps year one cost under $50 / month for the expected 2 to 5 users.
- Faster to build features later than no code platforms allow once we hit anything custom.

**Rejected**:

- **Retool**: Per user seat pricing scales badly. Less control over where data lives. Audit log primitives weaker.
- **Airtable**: Not PHIPA defensible for patient health information. No real RLS. Vendor controlled storage region.

## 2026 05 13. Region: Canada Central

**Decision**: All Supabase resources provisioned in Canada Central (ca central 1).

**Why**:

- PHIPA expects health information about Ontario residents to be processed in Canada where reasonable.
- Avoids cross border data transfer disclosures in client agreements.

**Rejected**:

- US East: cheaper egress to some services but creates a cross border data flow that we would have to document and defend.

## 2026 05 13. Budget cap: under $50 / month year one

**Decision**: Free tier for both Supabase and Vercel during year one. Upgrade triggered by an actual limit (database size, function invocations, build minutes), not by anticipation.

**Why**:

- Real usage is 2 to 5 internal users in year one. Free tier is more than enough.
- Forces us to keep payloads small and the schema clean.

**Rejected**:

- Pre buying Supabase Pro: would burn $25 / month before we hit any limit.

## 2026 05 13. Roles fixed to four

**Decision**: admin, coordinator, finance, viewer. Stored on a user_roles table, enforced in RLS.

**Why**:

- Maps to actual TKG job functions. Keeps RLS policies readable.
- Easier to audit "who can do what" with four named roles than with permission grids.

**Rejected**:

- Granular per resource permissions: overkill at this user count.
- Single role per user table column: harder to extend if we ever need multi role.

## 2026 05 13. Soft delete only, immutable audit logs

**Decision**:

- Every domain table has a `deleted_at timestamptz` column. Hard deletes are not allowed from the app.
- Audit log table is append only. Updates and deletes on the audit table are blocked at the database level (no UPDATE / DELETE grants, or a BEFORE trigger that raises).

**Why**:

- Contribution agreement reporting and ISC audits expect us to be able to reconstruct who did what and when, including for deleted records.
- PHIPA breach investigations also require a tamper evident trail.

**Rejected**:

- Hard deletes with a separate archive: easy to forget to archive, easy to lose the chain of custody.
