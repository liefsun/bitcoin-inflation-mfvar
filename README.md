# Bitcoin-Inflation Mixed-Frequency VAR

Replication code for Chapter 4 of *Bitcoin in the Macroeconomic Landscape: Price Determinants, Regime Dynamics, and Volatility Modelling*.

## Background

This chapter investigates the dynamic relationship between Bitcoin returns and consumer price inflation across three economies (United States, South Korea, Japan) using a Mixed-Frequency VAR framework. Daily Bitcoin returns are aggregated into five weekly sub-periods per month via the Ghysels (2016) stacking approach, then combined with monthly year-on-year CPI inflation rates to form an 8-variable VAR(2) system. The model is estimated with Newey-West robust standard errors and analysed through Generalised Impulse Response Functions (Pesaran & Shin, 1998) and Generalised Forecast Error Variance Decomposition.

## Data

| Variable | Source | Frequency | Series ID / File |
|----------|--------|-----------|------------------|
| BTC-USD close price | Yahoo Finance (`yfinance`) | Daily | `BTC-USD` |
| US CPI (seasonally adjusted) | FRED | Monthly | `CPIAUCSL` |
| South Korea CPI | FRED | Monthly | `KORCPIALLMINMEI` |
| Japan CPI | IMF International Financial Statistics | Monthly | `japan_cpi_imf.csv` |

- **Sample period**: January 2015 -- March 2023 (~99 months, 2,266 trading days)
- BTC daily returns are converted to five weekly sub-period cumulative log returns per month
- CPI series are transformed to year-on-year log changes: ln(CPI_t / CPI_{t-12})

## Repository Structure

```
ch4_mfvar/
├── replication_mfvar.ipynb   # Main replication notebook (all analysis)
├── japan_cpi_imf.csv         # Japan CPI index from IMF IFS (2012-01 to 2023-12)
├── requirements.txt          # Python dependencies
└── README.md                 # This file
```

## How to Run

1. **Python version**: 3.9+
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Open and run the notebook sequentially:
   ```bash
   jupyter notebook replication_mfvar.ipynb
   ```
4. US and Korean CPI data are fetched live from FRED; Japan CPI is loaded from the included CSV. An internet connection is required for the FRED download and BTC price retrieval via `yfinance`.

## Key Findings

- **Granger causality**: Bitcoin returns Granger-cause CPI inflation in all three countries (US p < 0.01, Korea p < 0.01, Japan p < 0.05) under both standard and Newey-West robust Wald tests.
- **Impulse responses**: A one-standard-deviation BTC shock produces a small positive pass-through to US and Japanese CPI at the 2-month horizon, while the Korean response is negative.
- **Variance decomposition**: BTC shocks explain approximately 7--11% of CPI forecast error variance at the 4-month horizon across all three countries.
- **Robustness**: Results are robust to alternative lag orders (VAR(1), VAR(3)), a pre-COVID sub-sample (2015--2019), and Toda-Yamamoto augmented causality tests that account for potential unit roots.
- **Bidirectional feedback**: US CPI shows marginal feedback to Bitcoin (p ~ 0.05), while significant cross-country CPI spillovers exist between the US and Korea.

## Thesis Reference

Chapter 4: *Bitcoin and Inflation Dynamics: A Mixed-Frequency VAR Analysis*
