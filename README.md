# Online Learning for Quantitative Finance

Academic research project at **CentraleSupélec / Université Paris-Saclay**, supervised by **Damien Challet (MICS)**. Final report: **4 June 2025**.

Online portfolio allocation with Follow-the-Leader, Follow-the-Regularized-Leader, Universal Portfolios and volumetric-barrier FTRL with quasi-Newton updates (VB-FTRL-qN). The repository collects the team report, research notebooks, implementation and experiments on synthetic and S&P 500 price series.

## Start here

- **[Final report (French)](reports/Projet_S8_Apprentissage_en_Ligne.pdf)** — mathematical background, algorithms and project findings across semesters S6–S8.
- **[Experiment notes](docs/EXPERIMENT_NOTES.md)** — reproduction status and limitations of the historical experiments.
- **[COP notebook](notebooks/archive/COP.ipynb)** — portfolio comparisons and allocation-distance plots on supplied market data.
- **[Universal Portfolio notebook](notebooks/archive/universal_portfolio_opti.ipynb)** — baseline, NumPy optimization and optional CuPy / PyTorch experiments.

## Repository layout

| Directory | Contents |
| --- | --- |
| `src/` | VB-FTRL implementation and synthetic return generators |
| `scripts/` | Synthetic, market-data and restart experiments |
| `notebooks/archive/` | Historical research notebooks, with saved outputs retained |
| `data/` | Supplied normalized S&P 500 price CSV |
| `reports/` | Original final team report |
| `docs/` | Attribution, dataset description and experiment caveats |

## Setup

Python 3.10+ is recommended. From the repository root:

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
python -m pip install -r requirements.txt
jupyter lab
```

Open a notebook under `notebooks/archive/`. A setup cell locates the repository root and makes `src/` importable. Dataset paths point to `data/`.

The NumPy sections require no GPU. CuPy and PyTorch are **optional**, installed separately for a compatible device; skip their cells otherwise. Market-download cells and `w_real_data.py` require internet access and return changing Yahoo Finance data.

```bash
python scripts/w_synthetic_data.py
python scripts/w_real_data.py
python scripts/w_synthetic_data_reboot.py
```

These are exploratory research experiments, not guaranteed one-command reproductions. Read the notes before running expensive grids or interpreting a historical chart. The VB-FTRL core is retained as supplied; numerical feasibility and theoretical correctness have not been re-established by this repository cleanup.

## Methods and experiments

- Online convex optimization, regret, FTL and regularization in the report.
- Discretized Universal Portfolio mixtures and optimized implementations.
- VB-FTRL-qN using affine simplex coordinates and vectorized matrix operations.
- Synthetic multiplicative returns and historical normalized equity prices.
- Wealth trajectories, allocation histories, L1 portfolio distances and exploratory restart heuristics.

The supplied `COP` experiment samples asset panels with seed 42 and compares parameter settings. Historical notebook outputs are retained for traceability; they are not newly validated performance claims.

## Attribution

S8 team: **Nabil Elyazidi, Victor Letournel, Javier Toro Berrios, Philémon Wehbe and Seif Zaafouri**. Earlier S6–S7 contributors and upstream Universal Portfolio code are credited in **[ATTRIBUTION.md](docs/ATTRIBUTION.md)** and the report. This is a collaborative academic project.
