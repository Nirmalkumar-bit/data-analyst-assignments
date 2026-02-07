# 📝 Project: The "Trust Index" – Analyzing Life Insurance Reliability in India (2018-2022)

## 1. Project Overview

**Role:** Senior Risk Analyst at a FinTech Insurance Aggregator
**Objective:**
Your company wants to update its recommendation engine to prioritize insurer reliability over just premium cost. Your goal is to analyze death claim settlement ratios and solvency metrics to identify the most trustworthy insurers in India, reducing customer complaints regarding rejected claims.

---

## 2. Resources & Links

* **Dataset Source:** [Life Insurance Death Claims Data India (2018-2022)](https://www.kaggle.com/datasets/bhanageviraj/life-insurance-death-claims-dataindia-2018-2022)
* **Target Files:** Focus on the files containing `DeathClaimTrends`, `IndividualDeathClaims`, or consolidated annual data sheets.
* **Documentation/Tools:**
* **Tool:** `Pandas` & `Matplotlib` – You will strictly use the built-in plotting capabilities of Pandas (which relies on Matplotlib) to demonstrate mastery of core Python libraries without external dependencies.
* [Pandas Visualization Documentation](https://pandas.pydata.org/docs/user_guide/visualization.html)



---

## 3. Detailed Task Instructions

### Phase 1: Ingestion & Data Quality Audit (The Foundation)

* **Task 1.1:** Load the dataset using Pandas. Be prepared to handle potential multi-header rows or merged cells if the source data was scraped from regulatory PDF tables.
* **Task 1.2:** **Identify "Dirty Data" Risks:**
* Check for percentage symbols (`%`) in numerical columns (e.g., "98.5%") that need to be stripped and converted to floats.
* Standardize Company Names: Ensure "HDFC Life" and "HDFC Standard Life" (or similar variations) are mapped to a single entity name to allow for accurate tracking over time.


* **Task 1.3:** Handle null values in key financial metrics (like `Solvency Ratio`). If a year is missing, decide whether to use forward-filling (ffill) assuming the ratio remained stable, or drop the row to preserve strict accuracy.

### Phase 2: Feature Engineering (The Senior Analyst Step)

* **Task 2.1:** Create 3 new columns to enhance the analysis:
* **`Rejection_Rate`**: Calculate `100 - Claim_Settlement_Ratio` to explicitly quantify the risk of non-payment.
* **`YoY_Growth`**: Calculate the Year-over-Year change in the Settlement Ratio for each company. (Is the company getting better or worse at paying claims?)
* **`Trust_Tier`**: Categorize companies based on their average Settlement Ratio:
* "Tier 1 (Elite)": > 98%
* "Tier 2 (Standard)": 95% - 98%
* "Tier 3 (Risk)": < 95%





### Phase 3: Exploratory Data Analysis (The "What" and "When")

* **Task 3.1 (Univariate - Distribution):** Use `df['Claim_Settlement_Ratio'].plot(kind='box')` or `df.boxplot()` to visualize the distribution across all companies. This will help you spot outliers (companies with dangerously low settlement rates).
*
* **Task 3.2 (Time/Trend):** Use `df.pivot().plot(kind='line')` to plot the `Claim_Settlement_Ratio` over the years (2018-2022).
* *Constraint:* Do not plot all companies at once. Filter for the "Top 5 Market Leaders" vs. "Bottom 5 Performers" to create a readable contrast.


* **Task 3.3 (Categorical):** Compare **Public vs. Private** sector insurers (if this column exists, otherwise manually tag the Life Insurance Corporation of India (LIC) vs. Private players). Use `df.groupby().mean().plot(kind='bar')` to compare their average Solvency Ratios.

### Phase 4: Advanced Analysis (The "Why" - Correlations & Patterns)

* **Task 4.1:** **Correlation Analysis (Scatter Plot):**
* Create a scatter plot using `df.plot.scatter(x='Solvency Ratio', y='Claim Settlement Ratio')`.
* *Goal:* Investigate the hypothesis: "Do companies with deeper pockets (higher solvency) actually pay claims more reliably?" Look for a positive correlation.


* **Task 4.2:** **Volatility Analysis:**
* Calculate the standard deviation of the `Claim_Settlement_Ratio` for each company over the 5-year period.
* *Goal:* Identify the "Most Consistent" insurers. A company with a 97% average but high volatility is riskier than a stable 96%.



---

## 4. Expected Deliverables & Output

Your final Jupyter Notebook must contain:

1. **Executive Summary:** A 3-point bulleted list highlighting the safest insurer, the most improved insurer, and the overall industry trend (positive or negative).
2. **Clean Visualizations:** Every chart must have a `title`, `xlabel`, and `ylabel` set using `plt.title()`, `plt.xlabel()`, etc.
3. **Business Logic:** Below each chart, add a Markdown cell answering:
* *"So what? If I am a customer purchasing a 30-year policy, why does this chart matter to me?"*


4. **Final Recommendation:** A specific recommendation strategy.
* *Example:* "We should badge insurers in the 'Tier 1' category as 'Verified Trustworthy' on our platform to increase conversion rates."



---

## 💡 Pro-Tips & Suggestions

* **Performance:** Since this dataset is small (aggregated data), focus on **code readability** and **narrative flow** rather than processing speed. Use clear variable names like `df_insurance_trends`.
* **Aesthetics:** Although you are using basic Pandas plotting, you can still make it look professional. Use `plt.style.use('ggplot')` or `plt.style.use('seaborn-v0_8-whitegrid')` at the top of your notebook to instantly improve the default chart styles.
* **The "Analyst Mindset":** In insurance, **consistency is key**. A company that had 99% settlement one year and 85% the next is a red flag. Don't just look at averages; look at the stability of the trend.

---
