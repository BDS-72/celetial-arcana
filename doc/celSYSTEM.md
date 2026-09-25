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

---

# Overview and Philosophy

**Canonical fact — naming:** this repository's local directory name in this
workspace is `celetial-arcana` (a typo of "celestial"), but its actual
product identity — the name in its own README and UI branding — is
**Celestia Arcana**. This `doc/system/` tree documents it as Celestia
Arcana. Treat `celetial-arcana` as a local workspace directory name only.

Celestia Arcana is a SvelteKit application combining a full 78-card tarot
deck with astrological birth-chart calculation and AI-generated synthesis
of the two into a single reading, with voice narration.

**Canonical fact:** the astrological-synthesis feature requires a Python
runtime alongside the SvelteKit app (`astro_tarot_reader.py` at the repo
root) — this is a hybrid Node/Python application, not a pure JavaScript
one. See `90-handover.md` for the deployment implication.

---

# Architecture

**Canonical fact:** Celestia Arcana is a SvelteKit application with a hybrid
JS/Python backend split across its own server routes:

- `src/routes/api/reading/+server.ts` — traditional tarot engine (pure
  TypeScript, card-drawing logic in `src/lib/tarot.ts`)
- `src/routes/api/ephemeris/+server.ts` — celestial-position calculations
  (`src/lib/ephemeris.ts`, using the Astronomy Engine library)
- `src/routes/api/astro-tarot/+server.ts` — astrological synthesis; this
  route shells out to the standalone `astro_tarot_reader.py` Python script
  at the repo root, per the README's deployment notes about Python being
  required
- `src/routes/api/combined-reading/+server.ts` — merges the traditional and
  astrological readings
- `src/routes/api/reading-explanation/+server.ts` — AI Q&A about a
  generated reading

**Canonical fact:** card definitions live in
`src/lib/decks/celestia-arcana.ts` (the full 78-card deck) and
`src/lib/decks/tarot-meanings-map.ts`. Card artwork lives under
`static/cards/`.

**Canonical fact:** voice narration selection logic lives in
`src/lib/utils/voiceSelection.ts`.

**Canonical fact:** all AI-backed routes (astro-tarot synthesis, reading
explanation) depend on `OPENAI_API_KEY` — see `05-config-env.md`.

---

# Tech Stack

**Canonical fact:**

- SvelteKit 2.0, Svelte 5 (confirmed directly in `package.json`: `svelte:
  ^5.55.9`)
- Tailwind CSS 4.0
- Bun (runtime/package manager; Node.js 18+ works as a fallback per the
  README)
- Python 3.6+ — required specifically for the astrological-synthesis
  feature, not for the app generally
- OpenAI API (GPT-4-family models) for AI synthesis
- Astronomy Engine — celestial-position calculations
- Motion — animation library
- Zod — validation

---

# Project Structure

```text
src/
  routes/
    +page.svelte                    Landing page
    reading/+page.svelte            Reading interface
    deck/+page.svelte                Card browser
    alignment/+page.svelte           Birth chart calculator
    dashboard/+page.svelte           AI dashboard
    api/
      reading/+server.ts             Traditional tarot engine
      astro-tarot/+server.ts         Astrological synthesis (shells out to Python)
      combined-reading/+server.ts    Merges traditional + astro readings
      ephemeris/+server.ts           Celestial calculations
      reading-explanation/+server.ts AI Q&A about a reading
      cards/, feedback/              Card data, feedback submission
  lib/
    components/     Card.svelte, ReadingFeedback.svelte, ReadingExplainer.svelte
    decks/           celestia-arcana.ts (full deck), tarot-meanings-map.ts
    utils/           voiceSelection.ts
    tarot.ts         Card-drawing logic
    ephemeris.ts     Astronomical calculations
static/
  cards/             78 tarot card images (WebP)
astro_tarot_reader.py   Standalone Python astrological engine, invoked by the astro-tarot route
```

---

# Configuration and Environment

**Canonical fact — required:**

- `OPENAI_API_KEY` — required for AI-synthesized readings and the
  reading-explanation feature.

**Canonical fact — optional:**

- `VITE_ASTRO_TAROT_MODEL` — overrides the OpenAI model used (default
  `gpt-4o-mini`; `gpt-4o` and `gpt-4-turbo` are also supported per the
  README).

**Canonical fact:** verify the local Python setup with
`bun run test:python` (or `npm run test:python`), which checks that Python
is detected, the `openai` and `requests` packages are installed, and the
API key is configured.

---

# API Routes

| Endpoint | Method | Description |
| --- | --- | --- |
| `/api/cards` | GET | Retrieve all tarot cards |
| `/api/reading` | POST | Generate a traditional tarot reading |
| `/api/astro-tarot` | POST | Generate astrological synthesis (requires Python) |
| `/api/combined-reading` | POST | Merge traditional + astro readings |
| `/api/ephemeris` | GET | Calculate celestial positions |
| `/api/reading-explanation` | POST | AI-powered reading Q&A |
| `/api/feedback` | POST | Submit reading feedback |

**Canonical fact:** `/api/astro-tarot` is the only route with a hard runtime
dependency on Python — see `90-handover.md` for the deployment
implication.

---

# Handover

**Canonical fact — deployment constraint:** because `/api/astro-tarot`
shells out to a Python script, this app **cannot run its full feature set
on serverless platforms without a Python runtime** (Netlify Functions,
Vercel Functions, per the repo's own README). Render, Railway, Fly.io, or a
traditional VPS are the supported options for the full feature set. Static
deployment (Netlify/Vercel) still serves traditional tarot readings, but
`/api/astro-tarot` will fail on those platforms.

**Canonical fact:** the repo ships `render.yaml` for one-click Render
deployment, the README's recommended path.

**Known limitation of this chapter set:** authored from the repo's own
README plus direct verification of the Svelte version, the API route file
layout, and the presence of `astro_tarot_reader.py`. Card-content details,
the exact synthesis pipeline logic inside the Python script, and voice
narration specifics were not independently re-derived from source — see
`src/lib/decks/celestia-arcana.ts` and `astro_tarot_reader.py` directly for
those.
