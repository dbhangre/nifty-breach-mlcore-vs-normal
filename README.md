# NIFTY Breach Prediction: ML-core vs Normal (Gaussian)

This repository supports my QM640 Data Analytics Capstone project at Walsh College.
The project asks a simple but important question:

> Can a machine-learning model predict whether the NIFTY 50 will breach a predefined upper or lower weekly price band better than the standard Gaussian formula, when both methods are given the same information?

The GitHub repository is maintained by **Dhyanendra Bhangre**:  
https://github.com/dbhangre/nifty-breach-mlcore-vs-normal

---

## 1. Project overview

Each weekly NIFTY 50 expiry cycle starts with a predefined **upper price band** and **lower price band**. These bands are based on selected sigma levels, meaning a chosen number of standard deviations from recent price movement.

A breach occurs when the index closes:

- above the predefined upper band, or
- below the predefined lower band

before weekly expiry.

The standard approach is to use the Gaussian, or Normal, model. This project tests whether a learning model can improve the breach prediction while using the **same input information** as the Gaussian model.

---

## 2. Research questions

| Research Question | Plain-language objective |
|---|---|
| RQ1 | Compare ML-core F1 against Gaussian F1 on the same test cycles |
| RQ2 | Check whether Gaussian errors are systematic or random |
| RQ3 | Check whether predictability differs by decision day and band side |
| RQ4 | Check whether sigma and window settings affect F1 |

---

## 3. Data

The project uses public daily NIFTY 50 index prices only.

Primary data source:

- NSE historical index data: https://www.nseindia.com/reports-indices-historical-index-data

The project does **not** use private data, personal data, options-chain data, open interest, futures, implied volatility, or macroeconomic data in Project 1.

---

## 4. Clean data dictionary

| Field | Description |
|---|---|
| Date | Trading date |
| Open | NIFTY 50 open price |
| High | NIFTY 50 daily high |
| Low | NIFTY 50 daily low |
| Close | NIFTY 50 closing price |
| daily_log_return | log(Close / previous Close) |
| realized_vol | Rolling observed volatility, shifted one day to avoid look-ahead |
| intraday_range | (High − Low) / Close |
| Volatility | Alias of realized_vol for pipeline compatibility |
| upper_breach | Target label: 1 if expiry price closes above upper band |
| lower_breach | Target label: 1 if expiry price closes below lower band |

---

## 5. Methodology guardrails

This project is designed to avoid common modelling mistakes:

- Walk-forward evaluation: train on the past and test on the future
- No test leakage: thresholds are not fitted on the test set
- Same inputs for both contestants: ML-core and Gaussian use the same price and volatility information
- Primary metric: F1, because breach events are relatively rare but important
- GitHub and exported artifacts allow reproducibility

---

## 6. Pipeline structure

Suggested project structure:

```text
nifty-breach-mlcore-vs-normal/
├── data/
│   ├── raw/
│   ├── clean/
│   └── cycles/
├── src/
│   ├── S0_Fetch_P1.py
│   ├── S0_Cleanup_P1.py
│   ├── S1_Config_P1.py
│   ├── S2_CycleBuild.py
│   ├── S3_Train_P1.py
│   ├── S3_Harvest.py
│   ├── S3_Select.py
│   ├── S6_InferEval_P1.py
│   ├── S7_Significance_P1.py
│   └── S8_Charts_P1.py
├── outputs/
│   ├── ledgers/
│   ├── configs/
│   ├── results/
│   └── charts/
├── README.md
└── requirements.txt
```

---

## 7. Run order

```text
S1_Config_P1
S0_Fetch_P1
S0_Cleanup_P1
S2_CycleBuild
S3_Train_P1
S3_Harvest
S3_Select
S6_InferEval_P1
S7_Significance_P1
S8_Charts_P1
```

---

## 8. Expected outputs

The project produces:

- master results ledger
- selected sigma/window configuration
- model comparison workbook
- F1 bootstrap significance table
- confusion matrices
- ROC curves
- sigma-window heatmaps
- ML-minus-Gaussian delta F1 heatmap

---

## 9. Project stages

| Stage | Output |
|---|---|
| Synopsis | Research design, hypotheses, sample size, methodology |
| Interim | First full model run, early results, fairness checks |
| Final | Final statistics, charts, interpretation, recommendations |

---

## 10. License

This repository is intended for academic use as part of the Walsh College QM640 Data Analytics Capstone.

