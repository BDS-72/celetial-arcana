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
