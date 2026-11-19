# F1 Analysis: what actually decides a race?

A beginner data-science project on Formula 1 results from 1950 to 2026. It explores the history, tests popular claims with shuffle tests, and builds a model that predicts finishing positions.

## The answer

**Mostly where a driver starts, and the car that got them there.**

- **The grid comes first.** Finishing order follows starting order more closely than ever (a grid-to-finish link of 0.70–0.77 since the 1990s). It's by far the model's most useful feature.
- **The car comes second.** Since 2000, the top team of each decade has won 47–49% of that decade's races, and team form is the model's next most useful feature.
- **The driver's own form adds only a little** once the grid and the team are known.
- **The popular stories barely matter.** Grid position isn't more important at Monaco, pit stops haven't gotten faster overall, the home crowd helps in qualifying but not in the race, and track specialists exist but the effect is small.

The model beats "finish = grid" across the whole field (2.28 places off against 2.49 on the 2023–2026 races), but not at the front: its pick won 56 of 89 races, against 54 for the pole sitter. Who wins among the front-runners comes down to things this data doesn't capture.

The full answer, limitations and next steps are in [`notebooks/05_conclusions.ipynb`](notebooks/05_conclusions.ipynb).

## Key results

| Question | Finding |
|---|---|
| Does the grid matter? | Yes, and more than it used to: the link went from 0.58–0.65 (1950s–1980s) to 0.70–0.77 (1990s on) |
| Do retirements still shake up races? | Much less: 48% of starters retired in the 1950s, 12% in the 2020s |
| Does grid position matter more at Monaco? | No: a link of 0.64 at Monaco against 0.65 elsewhere |
| Have pit stops gotten faster? | No, not in total time lost in the pit lane (2011–2026) |
| Is there a home advantage? | Partly: drivers start 0.23 places higher at home, but don't finish any better |
| Are there track specialists? | Yes, but the effect is small and mostly luck |
| Can a model beat "finish = grid"? | Slightly: 0.2 places closer per driver (not luck), with no gain at the front |
| What does the model rely on? | Grid position, then team form, then a little driver form |

## Notebooks

| Notebook | Part | What's in it |
|---|---|---|
| [`01_build_dataset`](notebooks/01_build_dataset.ipynb) | Setup | Joins the raw CSVs into one results table |
| [`02_explore`](notebooks/02_explore.ipynb) | Part 1 | Pole-to-win rates, retirements, dominant teams, grid vs. finish |
| [`03_test_claims`](notebooks/03_test_claims.ipynb) | Part 2 | Shuffle tests of four popular claims, with a findings table |
| [`04_predict`](notebooks/04_predict.ipynb) | Part 3 | A linear model vs. "finish = grid", feature importance, where the model fails |
| [`05_conclusions`](notebooks/05_conclusions.ipynb) | Part 4 | The answer, limitations and next steps |

The plan and progress are in [`OUTLINE.md`](OUTLINE.md).

## Running it

1. Create a virtual environment and install the packages: `python -m venv .venv`, then `.venv/bin/pip install -r requirements.txt`.
2. Run `01_build_dataset.ipynb` first. It builds `data/processed/results_joined.csv`, which isn't stored in git.
3. Run the other notebooks in order.

The notebooks read data from absolute paths under `/home/aris/projects/F1-Analysis/`. Change those if the repo lives somewhere else.

## Data

The F1 results dataset from Kaggle (November 2026 download), stored as CSVs in `data/raw/`.
