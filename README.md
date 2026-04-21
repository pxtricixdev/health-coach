# health-coach

A local-first health coaching plugin for [Claude Code](https://claude.com/claude-code). Three skills (nutrition, activity, sleep) that activate by context, plus two rituals (`/daily-check-in`, `/weekly-review`). All your data is stored as plain markdown on your own machine.

## What this is

A small marketplace with a single plugin. The plugin helps you log what you eat, how you train and how you sleep, then looks for patterns across all three. It's designed for self-coaching, not clinical use.

The coach keeps a short profile and a daily log per day. Everything is a markdown file under `plugins/health-coach/data/` — you can read, edit or delete any of it directly.

## Installation

Install it in Claude Code:

```
/plugin marketplace add pxtricixdev/health-coach
/plugin install health-coach@health-coach
```

For local development (before pushing, or if you're forking), install from a path:

```
/plugin marketplace add /absolute/path/to/health-coach
/plugin install health-coach@health-coach
```

## First use

No setup file to fill in. The first time you use any coach — whether you run `/daily-check-in` or just mention a meal, a workout or how you slept — the relevant skill will notice you don't have a profile yet and ask you a handful of quick questions. Under a minute. Only the basics plus the domain you're using.

Your profile lives at `plugins/health-coach/data/profile.md`. You can edit it by hand any time.

## How it works

Three skills activate automatically based on what you say:

- **nutrition-coach** — meal logging, rough macro estimates, meal ideas, weekly patterns.
- **activity-coach** — workout logging, Strava/Garmin CSV analysis, training load.
- **sleep-coach** — sleep tracking, consistency analysis, evidence-based sleep hygiene.

Two slash commands:

- `/daily-check-in` — quick morning check across all three domains.
- `/weekly-review` — pattern review across the last 7 days, including cross-domain connections.

Daily logs are written to `plugins/health-coach/data/YYYY-MM-DD.md`, one file per day, with sections for sleep, meals and activity all in the same file. That's what makes cross-domain analysis trivial.

## Privacy & data handling

> ⚠ **Your health data stays on your machine.**
>
> - All logs and your profile live under `plugins/health-coach/data/` on your local filesystem. Nothing is uploaded anywhere by this plugin.
> - Your messages to Claude are processed by Anthropic the same way any other Claude Code conversation is — subject to [Anthropic's privacy policy](https://www.anthropic.com/privacy). This plugin does not add any extra transmission of data.
> - The `data/` folder is listed in `.gitignore`. Even if you commit and push, your profile and logs won't leave your machine.
> - **If you fork or clone this repo**, double-check that your `.gitignore` still excludes `plugins/health-coach/data/*` before committing anything. A quick `git status` before `git add` is enough.

## Medical disclaimer

> ⚠ **This plugin is an educational/informational tool, not medical advice.**
>
> It does not diagnose, treat, or cure any condition. It should not be used as a substitute for consultation with a qualified healthcare professional. For eating disorders, injuries, persistent sleep problems, pregnancy, chronic illness, or any concerning symptom, please consult a doctor, registered dietitian, physiotherapist or sleep specialist as appropriate.
>
> By using this plugin you accept that any suggestions generated are general in nature, non-clinical, and used at your own discretion.

## Structure

```
health-coach/
├── .claude-plugin/
│   └── marketplace.json          ← marketplace catalog
├── plugins/
│   └── health-coach/             ← the plugin
│       ├── .claude-plugin/
│       │   └── plugin.json       ← plugin manifest
│       ├── skills/
│       │   ├── profile-template.md   ← shape of data/profile.md
│       │   ├── nutrition-coach/
│       │   ├── activity-coach/
│       │   └── sleep-coach/
│       ├── commands/
│       │   ├── daily-check-in.md
│       │   └── weekly-review.md
│       ├── data/                 ← YOUR logs live here (gitignored)
│       └── README.md
├── LICENSE
└── README.md
```

## Verifying changes (for contributors)

After editing any `SKILL.md`, start a new Claude Code session (or use `/plugin reload`) and test with natural phrases to confirm skills still activate. The description field is the main trigger — if a skill isn't activating as expected, revise the description to be more explicit about its triggering contexts.

## License

MIT — see [LICENSE](LICENSE).
