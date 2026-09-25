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
