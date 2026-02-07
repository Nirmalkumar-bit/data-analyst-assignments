# 📝 Project: Global Nutrition Economics: Mapping the Affordability of Healthy Diets

## 1. Project Overview

**Role:** Global Macroeconomic Analyst for a Non-Governmental Organization (NGO).

**Objective:** Identify regions where the cost of a healthy diet is rising fastest and analyze the gap between food costs and regional income levels. The goal is to provide data-driven recommendations for food subsidy programs and international aid prioritization.

---

## 2. Resources & Links

* **Dataset Source:** [Price of Healthy Diet - Clean](https://www.kaggle.com/datasets/hassanjameelahmed/price-of-healthy-diet-clean)
* **Target Files:** `price_of_healthy_diet.csv`
* **Documentation/Tools:** * **Seaborn:** Best for statistical visualizations like heatmaps and faceted grids.
* [Seaborn Documentation](https://seaborn.pydata.org/tutorial.html)



---

## 3. Detailed Task Instructions

### Phase 1: Ingestion & Data Quality Audit (The Foundation)

* **Task 1.1:** Load the data using `pd.read_csv()`. Identify if "Year" is being read as an integer or an object and convert it to a proper datetime format if necessary.
* **Task 1.2:** **Missing Value Strategy:** Use `df.isnull().sum()` to identify gaps. For this economic dataset, use the Pandas `.groupby()` and `.transform()` methods to fill missing values with the **median** of that specific country rather than a global average.
* **Task 1.3:** Check for outliers in the "Cost" column using the IQR (Interquartile Range) method. Document any countries that appear as extreme outliers.

### Phase 2: Feature Engineering (The Senior Analyst Step)

* **Task 2.1:** Create 3 new metrics using Pandas vectorization:
* **YoY_Growth:** Use `.sort_values()` followed by `.pct_change()` grouped by 'Country Name' to find the annual inflation rate of a healthy diet.
* **Cost_to_Income_Ratio:** (Optional/Simulated) Create a column representing the cost of the diet as a percentage of a $5.00/day poverty line.
* **Price_Volatility:** Calculate the Standard Deviation of prices for each country over the available time period.



### Phase 3: Exploratory Data Analysis (The "What" and "When")

* **Task 3.1 (Univariate):** Use `sns.histplot()` to show the distribution of diet costs globally. Overlay a KDE (Kernel Density Estimate) to show the "shape" of global food poverty.
* **Task 3.2 (Time/Trend):** Use `sns.lineplot()` with the `hue` parameter set to "Region" to show how different parts of the world have experienced price increases over time.
* **Task 3.3 (Categorical):** Create a **Horizontal Bar Chart** using `sns.barplot()` to show the top 20 countries with the highest price volatility.

### Phase 4: Advanced Analysis (The "Why" - Correlations & Patterns)

* **Task 4.1:** **Correlation Heatmap:** Use `df.corr()` and `sns.heatmap()` to see if there is a relationship between population size, year, and the cost of a healthy diet.
* *Goal:* Determine if more populous countries are better protected from price spikes due to economies of scale.


* **Task 4.2:** **Regional Faceting:** Use a Seaborn `FacetGrid` to create a "Small Multiples" chart. Each "facet" should be a different region, showing the distribution of diet costs within that region.
* *Goal:* Identify which regions have the most internal inequality in food pricing.



---

## 4. Expected Deliverables & Output

Your final Jupyter Notebook must contain:

1. **Executive Summary:** A 3-point bulleted list of your biggest findings at the very top of the file.
2. **Clean Visualizations:** Every chart must use `plt.title()`, `plt.xlabel()`, and `plt.ylabel()`. Ensure you use `plt.tight_layout()` to avoid overlapping labels.
3. **Business Logic:** Below each chart, add a Markdown cell answering: *"So what? How does this help the business/NGO?"*
4. **Final Recommendation:** A summary of which 3 regions are at the highest risk of food insecurity based on the price trends.

---

## 💡 Pro-Tips & Suggestions

* **Performance:** When calculating Year-over-Year changes in Pandas, always ensure your data is sorted by `['Country Name', 'Year']` before using `.shift()` or `.pct_change()`.
* **Aesthetics:** Use `sns.set_theme(style="whitegrid")` at the start of your notebook to give your charts a clean, professional look suitable for a portfolio.
* **The "Analyst Mindset":** Don't just report the price; report the *change*. In economics, the rate of change (inflation) is often more disruptive to a population than the absolute price.