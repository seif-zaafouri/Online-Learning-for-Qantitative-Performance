# Supplied market data

`SP500_normalized_prices.csv.xz` contains the exact CSV supplied with the project, compressed losslessly with xz. Pandas reads it directly; use `xz -dk data/SP500_normalized_prices.csv.xz` to extract the original CSV. The first column is `Date`; other columns are equity tickers and contain normalized price series with missing values.

COP computes price relatives as `prices[:, 1:] / prices[:, :-1]` and selects columns with complete histories before sampling panels. Filtering by complete histories can introduce selection / survivorship bias. The exact vendor extraction, adjustments and data usage terms are not documented in the supplied CSV; do not infer these from its name. Live Yahoo Finance scripts are separate experiments and need not reproduce this frozen file.
