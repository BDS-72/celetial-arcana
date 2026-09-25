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
