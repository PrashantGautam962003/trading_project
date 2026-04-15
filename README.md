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

## How to Use

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/yourusername/your-repo-name.git
    cd your-repo-name
    ```
2.  **Open in Google Colab:** Upload the notebook (`your_notebook_name.ipynb`) to Google Colab.
3.  **Run the Cells:** Execute the cells sequentially to reproduce the analysis. Ensure your `Dataset.csv` file is located in the specified `project_path` after mounting Google Drive.
4.  **Review Outputs:** Examine the plots, statistical outputs, and the generated `Trading_Performance_Report.pdf` for detailed insights.
5.  **Power BI Integration:** Use the exported CSV files (`processed_trading_data.csv`, `ticker_performance_metrics.csv`, `ticker_trade_effectiveness.csv`) to create interactive dashboards in Power BI.

## Requirements

-   Python 3.x
-   `pandas`
-   `numpy`
-   `matplotlib`
-   `seaborn`
-   `fpdf`

These can be installed using pip:

```bash
pip install pandas numpy matplotlib seaborn fpdf
Future Work
Implement more advanced machine learning models for Trade_PnL prediction.
Explore other technical indicators and their combinations.
Optimize the trading strategy based on the insights gained.
Conduct backtesting with out-of-sample data.
# High-Frequency Trading Data Analysis

## Project Overview
This project provides a comprehensive analysis of high-frequency trading data across multiple financial instruments. The primary goal was to provide insights into trading strategy performance, risk management, and the efficacy of various indicators. The analysis culminates in a structured report and prepared data, ready for further exploration and dashboard creation in tools like Power BI.

## Business Problem
Analyzing high-frequency trading data presents several challenges due to its volume, rapid changes, and the need to quickly identify profitable patterns and manage risk. Key challenges addressed in this project include:

*   Understanding the performance of a trading strategy across diverse financial instruments.
*   Assessing the risk-adjusted returns and maximum drawdowns for each ticker.
*   Evaluating the effectiveness of technical indicators, like RSI, in predicting trade outcomes.
*   Quantifying win rates and average profit/loss to identify strengths and weaknesses of the strategy.

## Solution Approach

### Step 1: Data Loading and Initial Preparation
Loaded raw high-frequency trading data from `Dataset.csv` into a pandas DataFrame. The `Transaction_Time` column was converted to UTC datetime objects to ensure proper time-series analysis and handle different timezones.

### Step 2: Data Cleaning and Feature Imputation (Python)
Identified and handled missing values in critical financial indicators (`Log_Return`, `Volatility_20m`, `Price_Gap`, `RSI_14m`) by imputing them with their respective column means. This ensures data completeness and reliability for subsequent analysis.

### Step 3: Exploratory Data Analysis (EDA)
Performed in-depth exploratory data analysis covering:

*   **Dataset Overview:** Confirmed the presence of four unique tickers (`ES=F`, `GC=F`, `ZN=F`, `INR=X`) and identified the data's time range (April 6-10, 2026) with a primary 1-minute transaction frequency.
*   **Descriptive Statistics:** Generated detailed descriptive statistics for all numerical features.
*   **Visualizations:** Created histograms for numerical feature distributions, a correlation matrix heatmap, box plots for `Trade_PnL` and `Log_Return` by Ticker, and time-series plots for `Cumulative PnL` and `Drawdown` by Ticker.

### Step 4: Performance Metrics and Strategy Effectiveness Calculation
Calculated key performance indicators (KPIs) for each ticker, including:

*   `Total_PnL`, `Sharpe_Ratio`, and `Max_Drawdown`.
*   `Win_Rate`, `Average_Win_PnL`, and `Average_Loss_PnL`.
*   A `Trade_Outcome` column was created to categorize trades as 'Win', 'Loss', or 'Break-Even'.

### Step 5: Indicator Efficacy Analysis
Investigated the relationship between the `RSI_14m` indicator and `Trade_PnL` using scatter plots to determine its predictive power and whether its efficacy varies across different tickers.

### Step 6: Reporting and Data Export
Generated a comprehensive PDF report (`Trading_Performance_Report.pdf`) summarizing the key findings and answers to research questions. The processed main DataFrame (`processed_trading_data.csv`) and aggregated performance metrics DataFrames (`ticker_performance_metrics.csv`, `ticker_trade_effectiveness.csv`) were exported to CSV files for easy integration with Power BI.

## Key Insights

*   **Numerical Feature Distributions:** `Log_Return` distributions centered around zero with 'fat tails' confirm the common financial characteristic of infrequent but significant price movements. The right-skewness of `Volume` and `Volatility_20m` indicates intermittent spikes in activity.
*   **Correlation Analysis:** Weaker correlations between price-related features/indicators and `Trade_PnL` suggest complex, non-linear relationships, implying the need for more sophisticated models.
*   **Risk-Adjusted Performance by Ticker:** `ES=F` showed the highest `Total_PnL` and best `Sharpe_Ratio` (0.019). `GC=F` had significant `Total_PnL` but the largest `Max_Drawdown` (-$15,781.59). `INR=X` and `ZN=F` were more stable but less profitable.
*   **Indicator Efficacy (RSI_14m):** The `RSI_14m` indicator alone did not show a strong linear relationship with `Trade_PnL` for any ticker, suggesting context-dependency or a need for combination with other indicators.
*   **Trading Strategy Effectiveness:** `GC=F` had the highest `Win_Rate` (48.7%) and largest `Average_Win_PnL` ($163.23), but also the largest `Average_Loss_PnL` ($-160.81). `ES=F` showed respectable `Win_Rate` (44.8%) with significant average PnLs. `ZN=F` had a low `Win_Rate` (22.0%) but a high number of `Break_Even_Trades` (3427 out of 6038).

## Research Questions Answered

### Research Question 1: How does the strategy's risk-adjusted performance vary across different tickers?

*   `ES=F` demonstrated the best risk-adjusted performance with the highest `Total_PnL` and `Sharpe_Ratio` (0.019).
*   `GC=F` was profitable but exhibited the largest `Max_Drawdown` (-$15,781.59).
*   `INR=X` and `ZN=F` presented lower `Total_PnL` and `Max_Drawdown`, indicating more conservative but less lucrative outcomes.

### Research Question 2: Volatility and Drawdown Impact

*   `GC=F`'s high `Total_PnL` was accompanied by significant `Max_Drawdown` (-$15,781.59), underscoring substantial risk exposure.
*   `ES=F` maintained a balanced risk-reward profile with a moderate `Max_Drawdown` (-$8,325.00) relative to its profitability.
*   `INR=X` and `ZN=F` showed low `Max_Drawdown` ($-71.75 and $-79.69 respectively), implying more stable but less dynamic trading environments.

### Research Question 3: How effective is the `RSI_14m` indicator in predicting `Trade_PnL`, and does its efficacy vary by ticker?

*   The `RSI_14m` indicator alone did not show a strong linear relationship with `Trade_PnL` for any ticker. Its predictive power is likely context-dependent or requires combination with other indicators.
*   Efficacy varied: `ES=F` and `GC=F` showed wider PnL ranges across RSI, while `INR=X` and `ZN=F` had much tighter, smaller PnL ranges.

### Research Question 4: Trading Strategy Effectiveness - Win Rate and Average PnL by Ticker

*   `GC=F` achieved the highest `Win_Rate` (48.7%) and `Average_Win_PnL` ($163.23), but also the largest `Average_Loss_PnL` ($-160.81).
*   `ES=F` had a solid `Win_Rate` (44.8%) with significant `Average_Win_PnL` ($127.89) and `Average_Loss_PnL` ($-119.84).
*   `ZN=F` had a low `Win_Rate` (22.0%) but a high number of `Break_Even_Trades` (3427 out of 6038).
*   The strategy was most effective for `ES=F` and `GC=F` due to the magnitude of winning trades.

## Tech Stack Used
| Tool | Purpose |
| :---- | :---- |
| Python (Pandas, NumPy, Matplotlib, Seaborn, fpdf) | Data Cleaning, EDA, Feature Engineering, Performance Metrics Calculation, Report Generation |

## Project Workflow
1.  Load raw trading data (`Dataset.csv`).
2.  Clean and preprocess data (datetime conversion, missing value imputation).
3.  Perform comprehensive Exploratory Data Analysis (EDA) and visualizations.
4.  Calculate and analyze key trading performance metrics and strategy effectiveness.
5.  Answer predefined business research questions based on the analysis.
6.  Generate a detailed PDF report of findings.
7.  Export processed data and aggregated metrics to CSV for Power BI.

## Files in This Repository
*   `your_notebook_name.ipynb`: The main Google Colab notebook containing all project steps.
*   `Dataset.csv`: The raw input data.
*   `Trading_Performance_Report.pdf`: The generated PDF summary report.
*   `processed_trading_data.csv`: The cleaned and preprocessed main DataFrame.
*   `ticker_performance_metrics.csv`: Aggregated performance metrics by ticker.
*   `ticker_trade_effectiveness.csv`: Aggregated trade effectiveness metrics by ticker.

## Business Recommendations
*   **Focus on ES=F:** Given its superior risk-adjusted returns, prioritize further strategy optimization and capital allocation for `ES=F`.
*   **Mitigate GC=F Risk:** While profitable, the high `Max_Drawdown` for `GC=F` warrants reviewing risk management techniques (e.g., tighter stop-losses, dynamic position sizing) for this ticker.
*   **Re-evaluate ZN=F & INR=X Strategies:** Investigate strategies for `ZN=F` and `INR=X` to move beyond frequent break-even trades or small profits, potentially by exploring different entry/exit logic or higher volatility assets.
*   **Enhance Indicator Usage:** Explore combining `RSI_14m` with other technical indicators or market context to improve its predictive power for `Trade_PnL`, as its standalone efficacy is limited.

## What This Project Demonstrates
This project reflects a strong command of data analytics principles applied to financial markets, including:

*   Handling and preprocessing high-frequency time-series data.
*   Performing robust data cleaning and imputation.
*   Conducting in-depth exploratory data analysis and visualization.
*   Calculating and interpreting core financial performance metrics (Sharpe Ratio, Max Drawdown).
*   Evaluating trading strategy effectiveness (Win Rate, Average PnL).
*   Generating comprehensive reports and preparing data for business intelligence tools.

## Author
Prashant Gautam
B.Tech, Electronics and Communication Engineering
IIT (ISM) Dhanbad

Aspiring Data Analyst | Data Science Enthusiast | Business Analytics
