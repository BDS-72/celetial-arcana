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
