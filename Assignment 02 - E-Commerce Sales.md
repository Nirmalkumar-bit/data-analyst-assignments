# 📝 Project: E-Commerce Operations Audit & Profitability Analysis

## 1. Project Overview

**Role:** E-Commerce Operations Analyst
**Objective:** Analyze transactional sales data to identify underperforming product categories and optimize regional inventory strategies, aiming to recover lost revenue from operational inefficiencies.

---

## 2. Resources & Links

* **Dataset Source:** [https://www.kaggle.com/datasets/prince7489/e-commerce-sales](https://www.kaggle.com/datasets/prince7489/e-commerce-sales)
* **Target Files:** `E-Commerce Sales.csv` (or the main CSV file provided in the download)
* **Documentation/Tools:**
* **Pandas:** The primary library for data manipulation.
* [Pandas User Guide](https://pandas.pydata.org/docs/user_guide/index.html)



---

## 3. Detailed Task Instructions

### Phase 1: Ingestion & Data Quality Audit (The Foundation)

* **Task 1.1:** Load the dataset using Pandas. Note that the file is likely a CSV. Check the shape (`.shape`) and the first 5 rows (`.head()`) to confirm the data loaded correctly.
* **Task 1.2:** Conduct a "Dirty Data" check. specifically, filter and check for negative values in the `Quantity` or `Unit Price` columns, which might indicate returns or data entry errors. Also, check if the `Order Date` column is actually read as a datetime object; if not, convert it.
* **Task 1.3:** Check for null values (`.isnull().sum()`). If the number of missing values is less than 5% of the total dataset, drop them. If it is higher, create a "Unknown" category for categorical columns.

### Phase 2: Feature Engineering (The Senior Analyst Step)

* **Task 2.1:** Create at least 3 new columns to enable deeper analysis:
* **`Total_Revenue`**: Calculate this as `Quantity` * `Unit Price`. (Note: If a `Sales` column already exists, validate it against this calculation).
* **`Order_Month`**: Extract the month and year from the `Order Date` (e.g., "2024-01") to allow for monthly trend analysis.
* **`Price_Segment`**: Use a lambda function to categorize `Unit Price` into 'Low', 'Medium', and 'High' buckets (e.g., Prices under 50 are 'Low', 50-150 are 'Medium', 150+ are 'High').



### Phase 3: Exploratory Data Analysis (The "What" and "When")

* **Task 3.1 (Univariate):** Visualize the distribution of `Total_Revenue` using a **Histogram**. This will help you understand if the business relies on many small purchases or a few large "whale" orders.
* **Task 3.2 (Time/Trend):** Group by `Order_Month` and sum the `Total_Revenue`. Visualize this trend using a **Line Chart** to identify seasonal peaks (e.g., holiday spikes).
* **Task 3.3 (Categorical):** Compare performance by `Category` (or `Sub-Category`). Create a **Bar Chart** showing Total Revenue by Category to identify your "Cash Cow" products.

### Phase 4: Advanced Analysis (The "Why" - Correlations & Patterns)

* **Task 4.1:** Perform a **Correlation Analysis** (using a Heatmap) between numerical variables like `Quantity`, `Unit Price`, and `Total_Revenue`.
* *Goal:* Determine if lower unit prices actually lead to significantly higher order quantities (Elasticity check).


* **Task 4.2:** **Pareto Analysis (80/20 Rule):** Group data by `City` or `Region` and calculate total revenue. Sort them to identify the top 20% of locations that contribute to 80% of the revenue. This helps focus marketing efforts.

---

## 4. Expected Deliverables & Output

Your final Jupyter Notebook must contain:

1. **Executive Summary:** A 3-point bulleted list of your biggest findings at the very top of the file (e.g., "Electronics Category drives 40% of revenue").
2. **Clean Visualizations:** Every chart must have a `title`, `xlabel`, and `ylabel`. Use a consistent color palette.
3. **Business Logic:** Below each chart, add a Markdown cell answering: *"So what? How does this help the business?"*
4. **Final Recommendation:** A clear "Strategy Insight" based on the data. (e.g., "Discontinue the 'Clothing' line in the 'West' region due to high volume but low profitability.")

---

## 💡 Pro-Tips & Suggestions

* **Performance:** If the `Order Date` parsing is slow, specify the `format` parameter in `pd.to_datetime()` to speed it up.
* **Aesthetics:** Use `seaborn` styles (e.g., `sns.set_theme(style="whitegrid")`) to instantly make your charts look professional and report-ready.
* **The "Analyst Mindset":** Don't just report numbers; report *anomalies*. If sales dropped in a specific month, explicitly point it out in your text and hypothesize *why* (e.g., "Post-holiday slump").