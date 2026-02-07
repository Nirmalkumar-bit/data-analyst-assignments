# 📝 Project: Market Alpha: Quantitative Portfolio & Volatility Analysis

## 1. Project Overview

**Role:** Junior Quantitative Analyst at "Apex Capital Management" (Hedge Fund)
**Objective:** You have been tasked with analyzing historical price movements of top-performing tech stocks to identify volatility patterns. The goal is to recommend a "defensive" vs. "aggressive" portfolio allocation strategy to the Portfolio Manager, potentially optimizing risk-adjusted returns by 15%.

---

## 2. Resources & Links

* **Dataset Source:** [Kaggle: Stock Market Dataset](https://www.kaggle.com/datasets/jacksoncrow/stock-market-dataset)
* **Target Files:** Do **not** try to load all files.
* Focus on the `stocks` folder.
* Select 5 specific "Tickers" to analyze for a comparative study (e.g., `AAPL.csv`, `MSFT.csv`, `GOOG.csv`, `AMZN.csv`, and `NFLX.csv`).


* **Documentation/Tools:**
* **Primary Library:** `Pandas` (for data manipulation and plotting).
* **Visualization Helper:** `Matplotlib` or `Seaborn` (standard libraries that power Pandas plotting).
* **Documentation:** [Pandas Visualization Documentation](https://pandas.pydata.org/pandas-docs/stable/user_guide/visualization.html)



---

## 3. Detailed Task Instructions

### Phase 1: Ingestion & Data Quality Audit (The Foundation)

* **Task 1.1:** Write a Python function that accepts a list of Ticker symbols (e.g., `['AAPL', 'MSFT']`), reads the individual CSV files, adds a column named `Ticker` to each, and concatenates them into a single Master DataFrame.
* **Task 1.2:** **Date Parsing & Sorting:** Ensure the `Date` column is converted to `datetime` objects and set as the Index. Sort the data by `Ticker` and then by `Date` to ensure time-series continuity.
* **Task 1.3:** **Gap Detection:** Financial data often has gaps (weekends/holidays). Check if there are any *unexpected* null values in the `Adj Close` or `Volume` columns. Fill them using "Forward Fill" (`ffill`) logic.

### Phase 2: Feature Engineering (The Senior Analyst Step)

* **Task 2.1:** Create 3 specific financial metrics:
* **Daily Return (%):** Calculate the percentage change in `Adj Close` from the previous day. (Tip: Use `.pct_change()`).
* **Moving Averages:** Calculate the `50_Day_MA` (Short-term trend) and `200_Day_MA` (Long-term trend) using `.rolling(window=x).mean()`.
* **Volatility (Risk):** Calculate a rolling 30-day standard deviation of the Daily Returns. This serves as a proxy for "Risk."



### Phase 3: Exploratory Data Analysis (The "What" and "When")

* **Task 3.1 (Univariate):** Visualize the distribution of **Daily Returns** for a single stock (e.g., AAPL).
* Use `df['Daily_Return'].plot(kind='hist', bins=50)` to create a histogram.
* *Goal:* Check if the data is Normally Distributed or has "Fat Tails" (extreme crash events).


* **Task 3.2 (Time/Trend):** Create a **Trend Line Chart** for one specific year of data.
* Use Pandas plotting to plot `Adj Close`, `50_Day_MA`, and `200_Day_MA` on the same chart.
* *Style Note:* Differentiate the lines (e.g., make the stock price a solid line and moving averages dashed).


* **Task 3.3 (Categorical/Comparative):** Create a Bar Chart comparing the **Total Cumulative Return** ((Final Price - Initial Price) / Initial Price) for all 5 selected stocks.
* Use `df.plot(kind='bar')` to compare the final performance.



### Phase 4: Advanced Analysis (The "Why" - Correlations & Patterns)

* **Task 4.1:** **Correlation Matrix:** Pivot your data so that columns are Tickers and rows are Dates, with values being `Daily Return`.
* Use `Seaborn.heatmap()` (or `df.corr().style.background_gradient()`) to visualize how these assets move together.
* *Goal:* Determine if these stocks move together (High Correlation = Low Diversification).


* **Task 4.2:** **Risk vs. Reward Scatter Plot:** Group by `Ticker` and calculate the Mean Daily Return (Reward) and the Standard Deviation of Daily Returns (Risk).
* Use a Scatter Plot (`df.plot.scatter(x='Risk', y='Reward')`) to place stocks on a risk/reward plane.
* *Goal:* Identify which stock offers the best "Sharpe Ratio" logic (High Return for Low Risk).



---

## 4. Expected Deliverables & Output

Your final Jupyter Notebook must contain:

1. **Executive Summary:** A 3-point bulleted list of your biggest findings (e.g., "Microsoft showed the highest risk-adjusted return") at the very top.
2. **Clean Visualizations:** Every chart must have a `title`, `xlabel`, `ylabel`. Use `plt.title()` or the `title='...'` argument inside the pandas plot function.
3. **Business Logic:** Below each chart, add a Markdown cell answering: *"So what? How does this help the Portfolio Manager?"*
4. **Final Recommendation:** A clear "Buy/Hold/Sell" strategy insight based on the Moving Average crossovers (Golden Cross vs. Death Cross).

---

## 💡 Pro-Tips & Suggestions

* **Performance:** Financial time-series calculations are vectorizable. Avoid `for` loops; use Pandas built-in vector functions (e.g., `df['Close'] * df['Volume']`) for speed.
* **Aesthetics:** Use `plt.style.use('ggplot')` or `plt.style.use('seaborn-v0_8')` at the top of your notebook to instantly make your Pandas charts look professional and publication-ready.
* **The "Analyst Mindset":** Focus on **Adjusted Close** (`Adj Close`) rather than `Close`. Adjusted Close accounts for stock splits and dividend payouts, which is the *true* return on investment for a shareholder.