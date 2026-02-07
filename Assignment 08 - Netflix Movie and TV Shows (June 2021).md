# 📝 Project: Netflix Global Content Strategy: Optimizing the Digital Library

## 1. Project Overview

**Role:** Content Acquisition & Programming Analyst

**Objective:** Identify high-performing content patterns to optimize Netflix’s multi-million dollar production budget. You must determine which genres, durations, and regional origins offer the best "long-tail" value for global subscriber retention using data-driven insights.

---

## 2. Resources & Links

* **Dataset Source:** [Netflix TV Shows and Movie List](https://www.kaggle.com/datasets/snehaanbhawal/netflix-tv-shows-and-movie-list)
* **Target Files:** `netflix_titles.csv`
* **Documentation/Tools:** * **Seaborn:** The standard for statistical data visualization in Python.
* [Seaborn Documentation](https://seaborn.pydata.org/)



---

## 3. Detailed Task Instructions

### Phase 1: Ingestion & Data Quality Audit (The Foundation)

* **Task 1.1:** Load the `netflix_titles.csv` using Pandas. Convert the `date_added` column to datetime format using `pd.to_datetime()`.
* **Task 1.2:** **Identify the "Sparse Data" risk:** Columns like `director` and `cast` have significant null values. Instead of dropping them, use `.fillna('Unknown')` to maintain the integrity of the rest of the row data.
* **Task 1.3:** Handle the `duration` column. Since it contains strings (e.g., "90 min" or "2 Seasons"), use Pandas string operations (`.str.split()`) to extract the numeric value into a new column, `duration_numeric`.

### Phase 2: Feature Engineering (The Senior Analyst Step)

* **Task 2.1:** Create at least 3 new columns from existing data that add business value.
* **Year Added:** Extract the year from `date_added` to perform time-series trends.
* **Major Genre:** The `listed_in` column often has multiple tags. Extract the first tag as the "Primary Genre" for cleaner grouping.
* **Content Age at Addition:** Subtract `release_year` from `year_added` to see if Netflix is prioritizing new releases or catalog classics.



### Phase 3: Exploratory Data Analysis (The "What" and "When")

* **Task 3.1 (Univariate):** Visualize the split between "Movie" and "TV Show" using a **Seaborn Countplot**.
* **Task 3.2 (Time/Trend):** Plot the count of content added per year using a **Line Plot**. This will show if the content library expansion is accelerating or slowing down.
* **Task 3.3 (Categorical):** Compare the **Top 10 Countries** by content volume using a **Bar Chart**. This highlights which markets are the primary content hubs for the platform.

### Phase 4: Advanced Analysis (The "Why" - Correlations & Patterns)

* **Task 4.1: Genre Heatmap**
* *Goal:* Create a **Heatmap** showing the relationship between `Rating` (TV-MA, PG-13, etc.) and `Primary Genre`. This reveals if certain genres are "pigeonholed" into specific age ratings (e.g., Are almost all Documentaries rated TV-G?).


* **Task 4.2: Seasonality of Content Drops**
* *Goal:* Use a **Histogram** or **Box Plot** to analyze which months see the highest volume of content additions. Is there a "holiday rush" for new titles?



---

## 4. Expected Deliverables & Output

Your final Jupyter Notebook must contain:

1. **Executive Summary:** A 3-point bulleted list of your biggest findings at the very top of the file.
2. **Static Visualizations:** Every chart must be rendered clearly using `%matplotlib inline` with a proper `plt.title()`.
3. **Business Logic:** Below each chart, add a Markdown cell answering: *"So what? How does this help a Content Exec decide what to greenlight next?"*
4. **Final Recommendation:** A clear "Strategy Insight" based on the data trends you've uncovered.

---

## 💡 Pro-Tips & Suggestions

* **Performance:** Use `df.info()` and `df.describe()` early on. Since this dataset is relatively small, Pandas will handle it easily, but these commands help you catch data type mismatches before you start plotting.
* **Aesthetics:** Use `sns.set_style("darkgrid")` or `plt.style.use('ggplot')` to make your Pandas/Matplotlib charts look portfolio-ready and less like "default" Excel charts.
* **The "Analyst Mindset":** Pay attention to the `release_year` vs. `date_added`. If you see a spike in old movies being added in a specific year, that's a "licensing deal" insight, not a production trend.

---
