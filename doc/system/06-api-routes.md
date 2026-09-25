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
