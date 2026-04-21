# Profile template

This is the canonical shape of `data/profile.md`. The three coach skills
(nutrition, activity, sleep) read this file at the start of every session.
If it doesn't exist, the active skill bootstraps it with a short interview
(ask only what's relevant to its own domain + the basics).

When generating `data/profile.md` for the user, copy the structure below
and only fill the sections for the domain you're bootstrapping. Leave the
other sections as empty placeholders so future skills know what to fill.

```markdown
---
name:
language:           # e.g. en, es, fr — match the user's preferred language
units: metric       # metric | imperial
created:            # YYYY-MM-DD
---

## Basics
- Age (optional):
- Height / weight (optional, for context):
- Main goal:
- Things to NOT harp on (e.g., weight, calorie counting):

## Nutrition
- Dietary preferences / restrictions:
- Allergies / intolerances:

## Activity
- Baseline (sessions per week, typical activities):
- Data sources (Strava, Garmin, Apple Health, none):

## Sleep
- Typical bedtime / wake time:
- Known issues (trouble winding down, early waking, etc.):
- Data sources (Apple Health, Oura, Whoop, Garmin, none):
```

## Bootstrap flow (for skills)

1. Check `data/profile.md`. If it exists, read it and continue.
2. If it doesn't, briefly tell the user: "I don't have your profile yet —
   mind if I ask a few quick questions? Takes under a minute."
3. Ask one question at a time. Only ask about your own domain plus the
   **Basics** block (name, language, main goal, things to avoid). Skip the
   rest — other skills will fill their own sections when first used.
4. Create `data/profile.md` with the template structure. Use today's date
   for `created`. Leave sections for other domains as empty placeholders.
5. Acknowledge briefly and continue with whatever the user originally
   asked about.

Notes:
- Never push for age, weight or measurements. All are optional.
- If the user declines to answer something, leave the field blank and
  move on.
- The profile file lives under `data/`, which is gitignored. Don't worry
  about committing it — the user's `.gitignore` keeps it local.
