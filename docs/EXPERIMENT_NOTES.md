# Experiment status and cleanup notes

## What changed in packaging

All ten supplied files are included. The report and two core modules retain their original bytes. The CSV is compressed losslessly as `.csv.xz`; decompression restores its original bytes. Notebooks retain original research cells and saved outputs; only a setup cell, a status banner and dataset paths were added. Scripts received repository-relative import setup, renamed generator imports, the `treshold` → `threshold` keyword correction, and `.w` access in the two restart wealth products. These compatibility edits do not validate the underlying algorithms.

## Known issues in the historical research

- In `COP.ipynb`, `wealth_bcrp` is called before its defining cell. Execute that definition first when exploring the archive. More importantly, its normalized terminal asset-growth weights are a heuristic: they do **not** solve the best constant rebalanced portfolio optimization problem. Historical BCRP labels should be read with that limitation.
- The archived simplex lattice construction has an off-by-one issue and can generate negative coordinates. Do not interpret its historical Universal Portfolio comparisons as a validated simplex-grid benchmark. A valid grid needs nonnegative coordinates summing to one.
- Historical Universal Portfolio and VB wrappers skip the first return in their wealth accounting, while some baselines include it. Align the evaluated periods before comparing returns. UP allocation histories are post-update, whereas VB histories are pre-update; align time indices for L1 comparisons too.
- Dense simplex grids grow combinatorially. The ten-asset grids in COP can be expensive in time and memory.
- The VB-FTRL implementation performs undamped updates, with no line search enforcing positive simplex coordinates or positive portfolio returns. Singular matrices, invalid denominators and infeasible weights are possible. Clipping weights afterwards in scripts does not establish correctness of intermediate optimization steps.
- `VB_FTRL` preallocates a maximum of 1,000 observations unless configured otherwise. Longer experiments must set `max_steps` explicitly or change the implementation.
- Synthetic and live-data scripts historically feed rescaled signed returns to a core using log-loss-style denominators. That convention requires mathematical review; synthetic runs can fail numerically. Restart rules are exploratory heuristics.
- The generator uses an unseeded RNG; plots vary between runs. COP panel selection is seeded separately.
- Saved outputs predate this cleanup. Full notebooks and network/GPU experiments have not been rerun end-to-end.

## Validation of this cleanup

Python source compilation and notebook schema validation are performed. A small positive-price-relative update smoke test checks the supplied core on a benign input only; it is not a proof of numerical stability or a financial backtest validation.
