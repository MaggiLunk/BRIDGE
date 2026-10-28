# BRIDGE — Standalone Artifact Plan

**v0.1.00 · 2026-10-28 · Status: DIRECTION SET BY BRIAN — build not yet commissioned**

## The correction (Brian, 2026-10-28 08:36 CDT)

BRIDGE does **not** live inside MOSAIC. The B1 read-only workspace built into the
MOSAIC artifact (`dashboard-grid-mosaic`, 2026-10-27) was a prototype placement,
not the destination. BRIDGE is a face of DASHBOARD (the Viewable Control Plane);
MOSAIC is only the tech it is designed with.

## What BRIDGE is

- **Its own artifact**, canonical name **`supa.bridge.*`** — first surface
  `supa.bridge.landing_page`. Registered under the `supa` label (BRIDGE serves
  the SUPA tower: the register, the legs, the log, the checklists).
- **Built with MOSAIC as a mosaic-doc**: the UI/UX is authored in MOSAIC tech
  (the MOSAIC interface system — palettes, canvas, footer readouts), then
  deployed as its own artifact. MOSAIC is the workshop, never the host.
- **CRUD for backend sockets**: BRIDGE connects UI/UX to DBs through Schema
  Sockets (DASHBOARD pattern: DB binding, CRUD, vault fields masked write-only,
  blocked deletes name the reason). B1's read-only seed becomes live reads;
  B2's request queue becomes real socket writes, executed by agents, verified
  by BRIDGE.
- **Live address: `gakz.magicwrx.com/bridge`** — served by Local's Web Server
  (same pattern as MOSAIC Route 1: GitHub source → Local serve → Lunk verifies).
  `gakz.magicwrx.com` is the GAKz-facing host; `/bridge` is its first route.

## Surfaces (from the locked BRIDGE spec, DASHBOARD §16.15 → v1.16.00 §3)

- PALETTE-LABELS (SIDEBAR-L) — the label register, bound from `supa.labels`
- CANVAS — two shores (GAKz DB ↔ GitHub) + crossing state IN SYNC / DRIFT /
  NOT MOVED, computed live from `supa.leg_versions`
- PALETTE-LEGS + PALETTE-LOG (SIDEBAR-R) — leg register + `supa.sync_log`
- FOOTER — verdict READOUTS (labels / in sync / drift / not moved)
- Actions: CHECK / REQUEST / OPEN — REQUEST writes a queued socket request;
  agents execute; BRIDGE verifies

## Data sockets (v1 scope)

| Socket | Target | Access |
|---|---|---|
| labels | `supa.labels` | read (+ steward writes) |
| legs | `supa.leg_versions` | read; record via REQUEST |
| log | `supa.sync_log` | read |
| registry | `supa.table_registry` | read |
| checklists | `checklist.*` | read (fleet now; per-entity as they appear) |
| artifacts | `supa.artifacts` | read |
| github | GitHub repos (heads, read-backs) | read, server-side only |

Server-side only: the browser never holds a GAKz service key (the MOSAIC
Stage 4 lesson — a static artifact cannot hold credentials; BRIDGE is a
fullstack artifact for exactly this reason).

## Path

- **A0** — Register the artifact: `supa.artifacts` row (slug `bridge`) +
  `checklist.fleet` row (all marks at start state). *Needs Brian's go.*
- **A1** — DASHBOARD doc amendment: §3 records BRIDGE as a standalone artifact
  at `gakz.magicwrx.com/bridge`; MOSAIC's embedded BRIDGE reclassified as the
  B1 prototype. Version bump + same-pass GitHub push per the Overall Rule.
- **A2** — Build: fullstack artifact, MOSAIC-tech UI (mosaic-doc), read
  sockets live against GAKz; seed snapshot retired (live reads only, every
  view stamped with its query time).
- **A3** — REQUEST queue (B2): socket writes as queued requests; agent
  execution + BRIDGE verification; CRUD opens per-socket as Brian approves.
- **A4** — Local serves `gakz.magicwrx.com/bridge` from the GitHub pin;
  Lunk verifies live vs GitHub vs register; MOSAIC's menu BRIDGE entry is
  retired to an OPEN-out link.

## Standing state until then

- B1 inside MOSAIC stays as-is — labelled prototype, snapshot data, harmless.
- The settled-`na` crossing question stays open and carries into the
  standalone build unchanged.
- BRIDGE's legs view (BRIDGE seed) and the stages view (`checklist.fleet`)
  remain two different views of the same register — neither replaces the other.
