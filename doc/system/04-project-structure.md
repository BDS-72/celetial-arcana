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
