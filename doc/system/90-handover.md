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
