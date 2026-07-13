# ETF Factor Rotation Project

## Overview

This project develops a Python-based ETF factor allocation framework. It analyzes four listed factor exposures (Value, Momentum, Quality and Low Volatility) and compares a dynamic allocation with three ETF-based alternatives: ITOT, LRGF and an equal-weight factor portfolio.

ITOT is used as the broad U.S. equity market benchmark. LRGF is used as an investable multifactor ETF comparator. The equal-weight portfolio provides a simple static allocation across the four selected factor ETFs.

The central question is practical: can listed factor ETFs be monitored and allocated through a transparent, benchmark-relative process? The answer is assessed through explicit rules rather than discretionary market views.

## Project Motivation

The project was designed to connect ETF-based asset management with applied portfolio analytics. ETFs are no longer only passive replication vehicles. They are also modular tools for portfolio construction, exposure management and reporting.

Factor ETFs are especially relevant in this context. They make investment styles such as Value, Momentum, Quality and Low Volatility accessible through listed products. This project uses these ETFs to build a systematic allocation and reporting framework.

The objective is not to create a predictive trading model. The goal is to show how ETF exposures can be compared, monitored and allocated in a clear and reproducible way.

## ETF Universe

| Role | ETF | Description |
|---|---|---|
| Value | VLUE | iShares MSCI USA Value Factor ETF |
| Momentum | MTUM | iShares MSCI USA Momentum Factor ETF |
| Quality | QUAL | iShares MSCI USA Quality Factor ETF |
| Low Volatility | USMV | iShares MSCI USA Min Vol Factor ETF |
| Benchmark | ITOT | iShares Core S&P Total U.S. Stock Market ETF |
| Multifactor Comparator | LRGF | iShares U.S. Equity Factor ETF |

## Methodology

The model uses daily adjusted ETF price data retrieved with `yfinance`. Daily returns are calculated from adjusted prices, which incorporate dividends and stock splits.

Each factor ETF is evaluated relative to ITOT using a composite active score. The score combines four dimensions:

- Information Ratio;
- Sharpe advantage;
- volatility advantage;
- drawdown advantage.

The active score is calculated as follows:

```text
Active Score =
40% × Information Ratio Score
+ 30% × Sharpe Advantage Score
+ 15% × Volatility Advantage Score
+ 15% × Drawdown Advantage Score
```

Each component is normalized cross-sectionally across the four factor ETFs. This allows variables expressed in different units to be combined into a single score.

The model uses a 252-trading-day rolling window. Portfolio weights are updated monthly. Factors are selected only when their active characteristics are positive. Positive scores are normalized into portfolio weights, with a maximum allocation cap per factor. Any residual allocation is assigned to ITOT.

Weights are shifted before being applied to returns. This means the strategy uses only information available at the time of allocation and reduces look-ahead bias.

## Outputs

The notebook produces:

- cumulative performance charts;
- annualized return, volatility, Sharpe ratio, maximum drawdown and Calmar ratio;
- rolling factor excess return analysis;
- monthly active allocation weights;
- comparison against ITOT, LRGF and an equal-weight factor portfolio;
- an automated monthly analytical factsheet;
- a professional project report.

## Main Findings

Over the comparable sample used in the report, the active allocation outperformed ITOT in annualized return and Sharpe ratio. The result is mainly return-driven rather than explained by a major reduction in volatility.

The analysis also shows that factor leadership changes over time. This supports the idea that factor ETFs can be monitored through a benchmark-relative framework. However, the model remains reactive. It observes historical factor characteristics and does not predict future factor leadership.

The value of the project lies in the clarity of the allocation process, the ETF implementation and the reporting framework. It should not be interpreted as evidence of persistent market-timing ability.

## Limitations

The project has several limitations:

- the analysis is based on one main parameter setting;
- no full robustness analysis is performed across alternative windows, caps or score weights;
- turnover and transaction costs are not explicitly estimated;
- ETF proxies are imperfect representations of academic factors;
- the risk-free rate is simplified at 0%;
- the attribution of performance by factor and period remains partial;
- historical results do not indicate future performance.

These limitations are discussed in more detail in the full report.

## Repository Structure

```text
ETF-Factor-Rotation-Project/
│
├── README.md
├── ETF_Factor_Rotation_Project.ipynb
├── requirements.txt
├── .gitignore
│
└── report/
    └── Elias_Banon_ETF_Factor_Rotation_Project_Report.pdf
```

## How to Run

Clone the repository and install the required packages:

```bash
pip install -r requirements.txt
```

Then open and run the notebook:

```text
ETF_Factor_Rotation_Project.ipynb
```

The notebook downloads ETF data, computes the allocation model, compares the strategies and generates the analytical outputs.

## Report

The full project report is available in the `report/` folder. It explains the motivation, methodology, results, limitations and contribution of the project in a professional format.

## Disclaimer

This project is an academic portfolio analytics exercise. It is not an investment recommendation, not a trading signal and not a fund marketing document.
