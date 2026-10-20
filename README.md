# Premier League Athlete Training Load Analysis

An exploratory analysis of two seasons of GPS and accelerometer data from Premier League training sessions (July 2021 to June 2023, 225 players across 8 teams). The aim is to detect when an athlete is "overreaching" in a session and to test whether those efforts relate to injury.

The full report, with code, figures and commentary, is in [`premier_league_athlete_training_load_analysis.html`](premier_league_athlete_training_load_analysis.html). The source notebook is [`main.ipynb`](main.ipynb).

## Approach

- **Data cleaning**: remove sessions shorter than 20 or longer than 120 minutes, and players with fewer than 20 recorded sessions.
- **Training intensity**: player load per minute, so sessions of different lengths can be compared.
- **Acute and chronic load**: 7-day and 28-day rolling measures of training intensity per player.
- **Overreaching indicators**: a week-on-week increase in acute intensity above 10%, and an acute:chronic workload ratio above 1.3.
- **Injury proxy**: a gap of more than 14 days between sessions is treated as an injury, attributed to the preceding session.
- **Result**: both indicators show a significant positive relationship with the number of injuries a player sustains (OLS, p < 0.001).

## Running it

Requires [uv](https://docs.astral.sh/uv/).

```bash
uv sync
uv run jupyter lab main.ipynb
```

To regenerate the HTML report:

```bash
uv run jupyter nbconvert --to html main.ipynb --output premier_league_athlete_training_load_analysis.html
```

## Data

`data/anonymous.csv` holds one row per player per session with duration, distance, player load, acceleration and deceleration counts, high-intensity and sprint distance, maximum velocity and change-of-direction counts. `data/Glossary.docx` defines each column. The data is anonymised and is used with permission.
