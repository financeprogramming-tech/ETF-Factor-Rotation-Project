# ETF Factor Rotation Project

## Overview

This project develops a Python-based ETF factor allocation framework. It analyzes four listed factor exposures — Value, Momentum, Quality and Low Volatility — and compares a dynamic allocation with three ETF-based alternatives: ITOT, LRGF and an equal-weight factor portfolio.

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
