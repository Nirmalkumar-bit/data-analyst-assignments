# 📝 Project: Omni-Channel Ad Performance & ROAS Optimization

## 1. Project Overview

**Role:** Digital Marketing Analytics Manager

**Objective:** Evaluate advertising efficiency across Google, Meta, and TikTok to identify high-performing channels and optimize budget allocation. You aim to maximize the Return on Ad Spend (ROAS) and reduce the Cost Per Acquisition (CPA) to improve the bottom line by 15%.

---

## 2. Resources & Links

* **Dataset Source:** [Kaggle: Global Ads Performance](https://www.kaggle.com/datasets/nudratabbas/global-ads-performance-google-meta-tiktok)
* **Target Files:** `global_ads_performance_dataset.csv`
* **Documentation/Tools:** * **Plotly Express:** For interactive marketing dashboards and cross-platform comparisons.
* [Pandas Documentation: Time-Series / Date functionality](https://pandas.pydata.org/docs/user_guide/timeseries.html)



---

## 3. Detailed Task Instructions

### Phase 1: Ingestion & Data Quality Audit (The Foundation)

* **Task 1.1:** Load the CSV dataset into a Pandas DataFrame and inspect the data types for all 14 columns (especially the `date` column).
* **Task 1.2:** **Data Integrity Check:** Marketing data often has calculation mismatches. Verify if the provided `CTR` (Clicks/Impressions) and `CPC` (Spend/Clicks) match the raw values. Ensure no rows have `impressions < clicks`.
* **Task 1.3:** Handle Nulls/Zeros: Check for rows where `ad_spend` is 0 but `clicks` or `conversions` are present. Decide whether to drop or impute these based on the 1,800-row sample size.

### Phase 2: Feature Engineering (The Senior Analyst Step)

* **Task 2.1:** Create 3 new columns to deepen the business context:
* **Cost Per Conversion (CPA):** Ensure this is calculated as `ad_spend / conversions` (handle division by zero).
* **Day of Week:** Extract from the `date` to see if performance spikes on weekends (TikTok) vs. weekdays (Google).
* **Conversion Efficiency:** Calculate `Conversions / Impressions` to see which platform is best at capturing "low-funnel" intent.



### Phase 3: Exploratory Data Analysis (The "What" and "When")

* **Task 3.1 (Univariate):** Use a **Box Plot** to visualize the distribution of `ROAS` across the three platforms. Identify outliers where campaigns significantly over-performed.
* **Task 3.2 (Time/Trend):** Plot a **Line Chart** of `ad_spend` vs. `revenue` over time. Use a 7-day rolling average to smooth out daily volatility and identify seasonal trends.
* **Task 3.3 (Categorical):** Create a **Grouped Bar Chart** comparing `Total Revenue` and `Total Spend` by `industry`. Which industries are "expensive" to compete in?

### Phase 4: Advanced Analysis (The "Why" - Correlations & Patterns)

* **Task 4.1:** **Multi-Platform Correlation Heatmap:** * *Goal:* Determine the relationship between `Impressions`, `Clicks`, `Spend`, and `Revenue`. Do more impressions always lead to more revenue, or is there a point of diminishing returns (ad fatigue)?
* **Task 4.2:** **Budget Reallocation Model:** Segment campaigns by `Platform` and `Campaign_Type`. Identify the "Underperformers" (High Spend, Low ROAS) and "Scalable Winners" (Low Spend, High ROAS).
* *Goal:* Provide a recommendation on how to shift 20% of the budget from the worst-performing platform to the best.



---

## 4. Expected Deliverables & Output

Your final Jupyter Notebook must contain:

1. **Executive Summary:** A 3-point bulleted list of your biggest findings (e.g., "TikTok Ads have the lowest CPC but Google Ads drive 40% higher conversion quality").
2. **Clean Visualizations:** Every chart must have a `title`, `xlabel`, and `ylabel`. Use a professional color palette (e.g., Google Blue, Meta Blue, TikTok Pink).
3. **Business Logic:** Below each chart, add a Markdown cell answering: *"So what? How does this help the marketing team decide where to spend the next $10,000?"*
4. **Final Recommendation:** A "2025 Media Plan" summary based on your data findings.

---

## 💡 Pro-Tips & Suggestions

* **Performance:** With 1,800 rows, memory isn't an issue. Focus on **Vectorization** (avoiding loops) to show you can write production-ready code.
* **Aesthetics:** Use `seaborn` or `plotly` to create "Brand-Specific" colors for the platforms to make your slides/notebook look like a professional agency report.
* **The "Analyst Mindset":** Don't just look at ROAS. High ROAS with very low volume is less useful than a moderate ROAS that can be scaled with more budget. Always look for the **Scalability** of a campaign.