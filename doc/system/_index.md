# Celestia Arcana — Compiled System Reference

**Designation:** cel
**Document role:** Canonical compiled technical reference for Celestia Arcana (local workspace directory: `celetial-arcana`)
**Source:** `doc/system/`
**Build command:** `bash doc/system/BUILD.sh`
**Document version:** 1.0 (2026-09-24) — initial doc/system authored from scratch
**Protocol:** BDS Documentation Protocol v2.0

> **Generated artifact warning:** `doc/celSYSTEM.md` is assembled output.
> Edit the source modules under `doc/system/` and rebuild. Hand edits to
> generated artifacts are overwritten by the next build.

**Naming note:** this repo's real product identity is **Celestia Arcana**.
The local workspace directory name `celetial-arcana` is a typo of
"celestial" and not the product's real name — see
`01-overview-philosophy.md`.

This `doc/system/` tree is the canonical source of truth for Celestia
Arcana. It uses explicit **truth classes**: canonical facts define role,
architecture, and the hybrid Node/Python runtime dependency; snapshot facts
are dated, audit-derived observations.

Assembly contract:

- Command: `bash doc/system/BUILD.sh`
- Validation: `bash doc/system/validate_snapshots.sh` runs during assembly
- Primary output: `doc/celSYSTEM.md`

| Part | File | Contents |
| --- | --- | --- |
| §1 | `01-overview-philosophy.md` | Purpose and the naming-alias disclosure |
| §2 | `02-architecture.md` | SvelteKit routes + Python astro-engine hybrid |
| §3 | `03-tech-stack.md` | Stack details |
| §4 | `04-project-structure.md` | Directory layout |
| §5 | `05-config-env.md` | Required/optional environment variables |
| §6 | `06-api-routes.md` | Route table |
| §7 | `90-handover.md` | Deployment constraint (Python required) |

## Quick Assembly

```bash
bash doc/system/BUILD.sh
```
