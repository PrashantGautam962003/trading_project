# High-Frequency Trading Data Analysis

## Project Overview

This project provides a comprehensive analysis of high-frequency trading data across multiple financial instruments. The primary goal was to provide insights into trading strategy performance, risk management, and the efficacy of various indicators. The analysis culminates in a structured report and prepared data, ready for further exploration and dashboard creation in tools like Power BI.

## Key Features

-   **Data Cleaning & Preprocessing:** Robust handling of data types (e.g., `Transaction_Time` conversion to UTC datetime objects) and missing values imputation for critical indicators (`Log_Return`, `Volatility_20m`, `Price_Gap`, `RSI_14m`).
-   **Exploratory Data Analysis (EDA):** In-depth exploration of data distributions, correlations, and time-series trends using descriptive statistics, histograms, correlation matrices, box plots, and line plots.
-   **Performance Metrics Calculation:** Detailed calculation of key performance indicators (KPIs) such as `Total_PnL`, `Sharpe_Ratio`, `Max_Drawdown`, `Win_Rate`, `Average_Win_PnL`, and `Average_Loss_PnL` for each financial instrument.
-   **Ticker-wise Analysis:** Comparative analysis of strategy performance, risk-adjusted returns, and indicator efficacy across different tickers (`ES=F`, `GC=F`, `ZN=F`, `INR=X`).
-   **Report Generation:** Automated generation of a comprehensive PDF report summarizing key findings and answers to predefined research questions.
-   **Data Export:** Export of processed data and aggregated metrics into CSV files for easy integration with external tools like Power BI.

## Data Description

The dataset `Dataset.csv` contains high-frequency trading data for four distinct financial instruments over a 5-day period (April 6-10, 2026), sampled at minute-level frequency. Key columns include:

-   `Transaction_Time`: Timestamp of the transaction.
-   `Open`, `High`, `Low`, `Close`: Price data.
-   `Volume`: Trading volume.
-   `Ticker`: Financial instrument identifier.
-   `Log_Return`: Logarithmic return of the asset.
-   `Volatility_20m`: Volatility over a 20-minute window.
-   `Price_Gap`: Price gap between consecutive trades.
-   `RSI_14m`: Relative Strength Index over 14 minutes.
-   `Risk_Limit_USD`: Risk limit in USD.
-   `Entry_Price`, `Exit_Price`: Prices at which trades were entered and exited.
-   `Trade_PnL`: Profit or Loss from a single trade.
-   `Slippage_USD`: Slippage incurred in USD.
-   `Cum_PnL`: Cumulative Profit or Loss.
-   `Peak`, `Drawdown`: Metrics related to peak cumulative PnL and drawdown.

## Key Findings

### 1. Numerical Feature Distributions: Unveiling Market Behavior

*   `Log_Return` distributions centered around zero with 'fat tails' confirm the common financial characteristic of infrequent but significant price movements—a key consideration for risk modeling. The right-skewness of `Volume` and `Volatility_20m` indicates that while most trading periods are relatively calm, there are intermittent spikes in activity and price fluctuation.

### 2. Correlation Analysis: Informing Model Complexity

*   Weaker correlations observed between price-related features and indicators like `Log_Return`, `Volatility_20m`, `RSI_14m`, and `Trade_PnL` suggest that simple linear relationships are not solely driving trade outcomes. This implies a need for more sophisticated, non-linear models or multi-factor analysis to accurately predict `Trade_PnL`.

### 3. Risk-Adjusted Performance by Ticker

*   `ES=F` showed the highest `Total_PnL` and the best `Sharpe_Ratio` (0.019), indicating the most favorable risk-adjusted returns.
*   `GC=F` generated significant `Total_PnL` but experienced the largest `Max_Drawdown` (-$15,781.59), highlighting its higher risk profile.
*   `INR=X` and `ZN=F` had much lower `Total_PnL` and `Max_Drawdown`, suggesting more stable but less profitable trading outcomes.

### 4. Indicator Efficacy (RSI_14m)

*   The scatter plot of `Trade_PnL` versus `RSI_14m` did not reveal a strong, simple linear relationship for any of the tickers. Its efficacy might be context-dependent or require combination with other indicators.

### 5. Trading Strategy Effectiveness (Win Rate and Average PnL)

*   `GC=F` had the highest `Win_Rate` (48.7%) and the largest `Average_Win_PnL` ($163.23), but also the largest `Average_Loss_PnL` ($-160.81).
*   `ES=F` had a respectable `Win_Rate` (44.8%) with significant `Average_Win_PnL` ($127.89) and `Average_Loss_PnL` ($-119.84).
*   `ZN=F` displayed a low `Win_Rate` (22.0%) but a very high number of `Break_Even_Trades` (3427 out of 6038), suggesting a strategy that frequently closes positions at or near entry price for this asset.
*   The strategy is most effective for `ES=F` and `GC=F`, driven by larger magnitudes of winning trades relative to losing trades.

## Research Questions Answered

### Research Question 1: How does the strategy's risk-adjusted performance vary across different tickers?

*   `ES=F` demonstrated the best risk-adjusted performance with the highest `Total_PnL` and `Sharpe_Ratio` (0.019).
*   `GC=F`, while profitable, exhibited the largest `Max_Drawdown` (-$15,781.59), indicating a higher risk profile.
*   `INR=X` and `ZN=F` presented lower `Total_PnL` and `Max_Drawdown`, suggesting more conservative but less lucrative outcomes.

### Research Question 2: Volatility and Drawdown Impact

*   `GC=F`'s high `Total_PnL` was accompanied by significant `Max_Drawdown` (-$15,781.59), underscoring substantial risk exposure.
*   `ES=F` maintained a balanced risk-reward profile with a moderate `Max_Drawdown` (-$8,325.00) relative to its profitability.
*   `INR=X` and `ZN=F` showed low `Max_Drawdown` ($-71.75 and $-79.69 respectively), implying more stable but less dynamic trading environments.

### Research Question 3: How effective is the `RSI_14m` indicator in predicting `Trade_PnL`, and does its efficacy vary by ticker?

*   The `RSI_14m` indicator alone did not show a strong linear relationship with `Trade_PnL` for any ticker, suggesting its predictive power is context-dependent or requires combination with other indicators. Its efficacy varied, with `ES=F` and `GC=F` showing wider PnL ranges across RSI, while `INR=X` and `ZN=F` had much tighter, smaller PnL ranges.

### Research Question 4: Trading Strategy Effectiveness - Win Rate and Average PnL by Ticker

*   `GC=F` achieved the highest `Win_Rate` (48.7%) and `Average_Win_PnL` ($163.23), but also the largest `Average_Loss_PnL` ($-160.81).
*   `ES=F` had a solid `Win_Rate` (44.8%) with significant `Average_Win_PnL` ($127.89) and `Average_Loss_PnL` ($-119.84).
*   `ZN=F` had a low `Win_Rate` (22.0%) but a high number of `Break_Even_Trades` (3427 out of 6038), suggesting a strategy that frequently closes positions near the entry price for this asset.
*   The strategy proved most effective for `ES=F` and `GC=F` due to the magnitude of winning trades.

## Project Structure

The project notebook (`your_notebook_name.ipynb`) contains the following main sections:

1.  **Data Loading and Setup**: Mounts Google Drive, sets up the working directory, and loads the raw data.
2.  **Data Cleaning and Preprocessing**: Handles missing values and converts data types.
3.  **Exploratory Data Analysis (EDA)**: Provides an overview of the dataset, descriptive statistics, and various visualizations.
4.  **Performance Metrics and Strategy Effectiveness**: Calculates and visualizes key trading performance metrics.
5.  **Key Findings and Research Questions Answered**: Summarizes insights and addresses the research questions.
6.  **Report Generation and Data Export**: Generates a PDF report and exports processed data to CSV files.

