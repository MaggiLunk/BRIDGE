# BRIDGE — the GAKz ↔ GitHub interface inside MOSAIC

**Status:** LOCKED 2026-10-26 — spec of record is DASHBOARD §16.15
(v1.15.00); this draft fed that section.
**Home (recommended):** a MOSAIC workspace — same pattern as the LOOP-closer
workspace (DASHBOARD §16.14): bound to live data, never copied (§16.10).

## What BRIDGE is

The control plane for the whole SSOT system, in one MOSAIC screen:
every product (LABEL) with its two stores of record side by side —
**GAKz (data)** on one side, **GitHub (source)** on the other — and the
sync state between them: versions per leg, last verified counts, drift.

If SUPA is the log and MESH is the map, BRIDGE is the **switchboard**:
you look at it to answer "is everything in sync?" and you act from it
to fix what isn't.

## Layout (MOSAIC structure, D12 vocabulary)

- **SIDEBAR-L — PALETTE-LABELS:** every label (PIX.MOV, MESH, MOSAIC,
  DASHBOARD, SUPA, LAT, MUSIC, WEBSERVER…) as rigid VOCAB items. Select a
  label → CANVAS + SIDEBAR-R rebind to it.
- **CANVAS — the two shores + the crossing:** left column = GAKz leg
  (schema, table count, row counts, last fill + its session, registry
  completeness), right column = GitHub leg (repo, head commit, VERSION,
  last push + read-back status), centre = the crossing state per artefact
  pair: **IN SYNC** (gold) / **DRIFT** (red, with both values shown —
  never a fake green, RULEBOOK §9.4) / **NOT MOVED** (grey, with the
  missing leg named). The MESH graph view can dock here as a canvas mode
  (the §16.14 pattern) — BRIDGE rows light their MESH nodes.
- **SIDEBAR-R — PALETTE-LEGS:** the five legs (GITHUB · SERVER · AGENT ·
  LIVE · DB) with `v00.00.00` per leg from `supa.leg_versions`, plus
  PALETTE-LOG: the live `supa.sync_log` stream for the selected label.
- **FOOTER — verdict READOUTS:** LABELS · IN SYNC n · DRIFT n · NOT MOVED n ·
  LAST CHECK (timestamp + who ran it). One glance = fleet truth.

## Data — bound, never copied (§16.10)

BRIDGE holds **bindings only**. Sources of record:
- GAKz: `supa.labels`, `supa.table_registry`, `supa.leg_versions`,
  `supa.sync_log`, `supa.repos`, `supa.artifacts`, per-schema counts
  (live queries / registered count views), `mesh.nodes/edges` for the map mode.
- GitHub: repo heads + VERSION files via read APIs, refreshed on check —
  displayed with their check timestamp, labelled STALE when old.
- Interface state (selected label, arrangement) → `dashboard.layouts`,
  per D12. BRIDGE itself creates no new tables in v1.

## Actions — request + verify; agents execute

The artifact cannot push to GitHub or run migrations itself (same
boundary as the PIX bridge). BRIDGE v1 actions therefore **queue +
verify**, exactly like FLOW's NEW queue:
- **CHECK** — re-read both shores now (counts, heads, versions), stamp
  the check, surface drift. (Read-only; safe to run any time.)
- **REQUEST PUSH / REQUEST FILL / REQUEST RESCAN** — writes a queued
  request row (a `supa.sync_log`-adjacent queue or the product's
  handoff INBOX) that Lunk or Local picks up under claim discipline,
  executes, and reports back with evidence; BRIDGE shows the request
  until its verification lands, then flips it IN SYNC.
- **OPEN** — deep links: the repo, the GAKz table (DB Interface), the
  product's handoff STATUS.
Write-actions that execute directly from the UI (real pushes from the
browser) are a later phase and a separate Brian call — they cross the
agent-execution boundary the whole fleet protocol is built on.

## Build phases

- **B0 — Spec lock:** Brian locks BRIDGE (+ any vocabulary: SHORE?
  CROSSING? — proposed only) → DASHBOARD §16.15 + Vocabulary, same-pass
  library.db + GAKz `lat.documents` sync + GitHub push (the standing rule).
- **B1 — Read-only BRIDGE:** MOSAIC workspace with the four regions above,
  bound to GAKz `supa.*` + GitHub read checks, seeded with the three
  moved products (PIX.MOV, MESH, MOSAIC) — MOSAIC's own row will honestly
  read NOT MOVED on both legs until its move lands.
- **B2 — Request queue:** REQUEST actions + agent pickup loop.
- **B3 — Map mode:** MESH graph docked as a canvas mode (reuses §16.14).

## Why this shape (recommendation)

BRIDGE as a MOSAIC workspace, not a new standalone artifact: the data,
the vocabulary, and the workspace machinery already exist; a new artifact
would fork all three. It also gives MOSAIC its first **bound** workspace —
which is the same missing piece as MOSAIC's own data move (localStorage →
`dashboard` tables), so B1 doubles as the proof of the MOSAIC bridge
pattern the PIX cutover needs.
