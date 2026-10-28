# BRIDGE — supa.bridge.*

The switchboard of the BIZ fleet: every label with its two stores of
record side by side — **GAKz (data)** ↔ **GitHub (source)** — and the
sync state between them. If SUPA is the log and MESH is the map, BRIDGE
is where you look to answer "is everything in sync?" and act to fix
what isn't.

- **Canonical name:** `supa.bridge.*` — first surface
  `supa.bridge.landing_page`. A face of DASHBOARD (the Viewable Control
  Plane), designed with MOSAIC tech. BRIDGE is **not** a room inside the
  MOSAIC artifact; the in-MOSAIC workspace is a retired prototype.
- **Reference implementation:** the Muse fullstack artifact `bridge`
  (live, seeded from the GAKz register; REQUEST queue writes real queued
  rows). It runs on the Muse artifact runtime and cannot be exported
  as a file — this repo carries its spec, plan, and seed so the surface
  can be stood up on the Web Server, Route 1 style.
- **Target:** **https://gakz.magicwrx.com/bridge** (Local's Web Server).
- **Data:** bindings only, never copies — GAKz `supa.*` register
  (labels, leg_versions, sync_log, table_registry, artifacts, repos) +
  `checklist.*`, read server-side; GitHub heads read server-side.
  Crossing rule **STRICT**: IN SYNC requires all five legs recorded and
  in sync; otherwise DRIFT (a recorded mismatch, both values shown) or
  NOT MOVED.

## Contents

- `BRIDGE-SPEC.md` — the locked spec (fed DASHBOARD §16.15 → v1.17.00 §3)
- `BRIDGE-ARTIFACT-PLAN.md` — the standalone-artifact plan (A0–A4)
- `bridge-seed.json` — the register snapshot the artifact was seeded
  from (19 labels / 51 legs / 10 log entries); verification baseline and
  fallback — live GAKz reads supersede it
- `STANDUP.md` — the Local Web Server standup instructions

**Status:** Muse artifact live (Brian's click-through pending);
Web Server standup dispatched 2026-10-28 — see `STANDUP.md`.
