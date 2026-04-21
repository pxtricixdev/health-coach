# health-coach plugin

Local-first coach for nutrition, physical activity and sleep. Works with manual entries or CSV exports from Apple Health, Garmin, Strava and Oura.

## What's inside

Three skills that activate automatically based on conversation context:

- **nutrition-coach** — meal logging, macro estimates, meal planning, weekly patterns.
- **activity-coach** — workout logging, Strava/Garmin CSV analysis, training load monitoring.
- **sleep-coach** — sleep tracking, consistency analysis, evidence-based sleep hygiene.

Two slash commands for rituals:

- `/daily-check-in` — quick morning check-in across all three domains.
- `/weekly-review` — weekly pattern review with cross-domain connections.

## How data is stored

One markdown file per day at `data/YYYY-MM-DD.md`. Sleep, nutrition and activity entries all go into the same daily file, which makes cross-domain analysis trivial.

Your baseline profile (goals, preferences, data sources) lives at `data/profile.md`. It's created the first time any coach runs — the skill asks you a short set of questions and generates the file. See [skills/profile-template.md](skills/profile-template.md) for the exact shape.

## Disclaimers

This is an **informational assistant**, not a medical professional. For anything clinical — eating disorders, injuries, persistent sleep problems, pregnancy, chronic conditions — see a qualified professional. The skills are written to flag these cases and defer, but ultimately the responsibility is on the user.

## Privacy

All your profile and log files live under `data/`, which is gitignored at the repo root. Nothing leaves your machine through this plugin. See the top-level [README](../../README.md#privacy--data-handling) for full details.
