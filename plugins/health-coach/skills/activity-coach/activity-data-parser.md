# Strava / Garmin CSV parsing

## Getting the data

### Strava
Account → Settings → "Get started" under "Download or Delete Your Account" → choose "Download Request". Email arrives with a ZIP containing `activities.csv`.

### Garmin Connect
garmin.com → Data Management → "Export your data". Includes activity files (FIT) and a summary CSV.

### Apple Health
iPhone → Health app → profile → "Export All Health Data". Produces an XML (not CSV). For this skill, it's easier if the user exports specific data via a shortcut or third-party app to CSV, OR just syncs to Strava.

## Columns to look for

Strava's `activities.csv` typically has (names vary slightly by export date):

| Column                  | What it means                              |
| ----------------------- | ------------------------------------------ |
| Activity Date           | Start date/time of the session             |
| Activity Type           | Run, Ride, Swim, Walk, Workout, etc.       |
| Elapsed Time            | Total time including pauses (seconds)      |
| Moving Time             | Time actually moving (seconds)             |
| Distance                | km (or meters depending on export)         |
| Average Heart Rate      | bpm                                        |
| Max Heart Rate          | bpm                                        |
| Elevation Gain          | meters                                     |
| Average Speed           | m/s                                        |
| Relative Effort         | Strava's suffer score (if HR available)    |

## What to compute

For a week of data, the useful aggregates are:

- **Total time** across all activities.
- **Session count** by type.
- **Intensity split** — if HR data exists, what % of time was in each zone (see `training-zones.md`). If not, ask the user to estimate RPE per session.
- **Consistency** — how many days had any activity.
- **Biggest day** — longest or hardest session, to check for pattern of too many hard days.

## Red flags to surface

- 3+ consecutive hard days (high HR, long duration) with no easy or rest day.
- Sudden jump in weekly volume (>15% vs previous week).
- Declining pace at same HR over multiple sessions → possible fatigue.
- Missing data / zero activity for 5+ days without context (might be illness, travel, or burnout).

Always ask before diagnosing — the data rarely tells the full story.
