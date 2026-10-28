# BRIDGE — Web Server Standup (for Local Agents)

**Target:** https://gakz.magicwrx.com/bridge — a new vhost on the Local
Web Server; `/bridge` is its first route.
**Working record:** GAKz table `checklist.fleet`, the BRIDGE row.

## What you are standing up

The BRIDGE surface from `BRIDGE-SPEC.md`, served Route 1 style (GitHub
source → your serve → Lunk verifies), bound to **live data sockets** —
not the snapshot. The Muse fullstack artifact `bridge` is the
reference implementation; it runs on the Muse artifact runtime and
cannot be exported as a file, so this standup is a server-side serve of
the same surface against the same data, per `BRIDGE-ARTIFACT-PLAN.md`
step A4.

## Data sockets (server-side only)

Read through your server-side proxy to GAKz (Supabase project
`gakzrwhxcpjbaqdvelft`), PostgREST profile headers per schema:

| Socket | Source | Access |
|---|---|---|
| labels | `supa.labels` | read |
| legs | `supa.leg_versions` | read |
| log | `supa.sync_log` | read |
| registry | `supa.table_registry` | read |
| artifacts / repos | `supa.artifacts`, `supa.repos` | read |
| checklists | `checklist.*` | read |
| github | GitHub repo heads + VERSION files | read, server-side only |

- **Key custody:** the service-role key lives in your server environment
  only — it arrives by Brian's hand or the vaulted path, never in chat,
  never in this repo, never in a log, never in the browser. If you don't
  have it, say so and stop at the vhost boundary; do not substitute
  another credential.
- **Crossing rule STRICT:** IN SYNC requires all five legs recorded +
  in sync; otherwise DRIFT (recorded mismatch — show both values) or
  NOT MOVED. Never render a fake green.
- **Verification baseline:** `bridge-seed.json` in this repo (19 labels
  / 51 legs / 10 log entries; footer LABELS 19 · IN SYNC 0 · DRIFT 1 ·
  NOT MOVED 18 at seed time). Live reads supersede the seed; if your
  live numbers differ from the seed, report both — that is drift
  information, not an error to hide.

## REQUEST queue

REQUEST (push / fill / rescan) writes a **queued request** that agents
pick up under claim discipline, execute, and report back with evidence;
the surface shows the request until its verification lands. Standup
scope: persist queued requests server-side (a `supa.sync_log`-adjacent
queue table or store you name in your report) — do not execute pushes
or fills from the web surface itself.

## Report back (verified facts only)

- Vhost + cert status · the URL answering 200 · what you served.
- One live read per socket (e.g. labels count from `supa.labels` through
  your proxy) proving the bindings are live, not seeded.
- Where queued REQUESTs persist.
- Anything that deviated, stated as drift with expected vs actual.

After your report, Lunk verifies the live surface against the GAKz
register and this repo. The `checklist.fleet` BRIDGE marks change only
on verified evidence + Brian's click-through of the Muse artifact.
