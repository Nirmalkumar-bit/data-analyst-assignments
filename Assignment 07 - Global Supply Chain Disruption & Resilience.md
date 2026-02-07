# 📝 Project: Operation Resilience: Global Supply Chain Stress-Testing

## 1. Project Overview

**Role:** Senior Supply Chain Operations Analyst

**Objective:** You are tasked by the Global Operations Director to evaluate the impact of external disruptions (natural disasters, geopolitical shifts) on logistics performance. The goal is to identify high-risk nodes in the supply chain and recommend inventory buffer strategies to reduce lead-time variability by 15%.

---

## 2. Resources & Links

* **Dataset Source:** [Kaggle: Global Supply Chain Disruption and Resilience](https://www.kaggle.com/datasets/bertnardomariouskono/global-supply-chain-disruption-and-resilience)
* **Target Files:** `supply_chain_data.csv` (Primary dataset containing shipment details, disruption types, and lead times).
* **Documentation/Tools:** * **Geopandas:** Essential for mapping the geospatial impact of disruptions across global routes.
* [Pandas Documentation: Time Series / Date functionality](https://pandas.pydata.org/docs/user_guide/timeseries.html)



---

## 3. Detailed Task Instructions

### Phase 1: Ingestion & Data Quality Audit (The Foundation)

* **Task 1.1:** Load the dataset using Pandas. Since supply chain data often includes various encodings, ensure you check for `utf-8` or `latin-1` if standard loading fails.
* **Task 1.2:** **Integrity Check:** Audit the `Lead_Time` and `Cost` columns for "impossible" values (e.g., negative days or zero costs on international shipments). Standardize the `Disruption_Type` categories to ensure "Natural Disaster" and "Natural_disaster" are treated as the same entity.
* **Task 1.3:** Handle missing values in the `Supplier_Rating` or `Delay_Reason` columns. If `Delay_Reason` is null where no delay occurred, fill with "On-Time Delivery" to maintain data distribution.

### Phase 2: Feature Engineering (The Senior Analyst Step)

* **Task 2.1:** Create 3 high-value features to measure resilience:
* **Disruption Intensity Score:** A calculated metric combining `Disruption_Duration` and `Impact_Level` to rank the severity of events.
* **Route Efficiency Ratio:** Calculate `Actual_Lead_Time / Planned_Lead_Time` to identify chronically underperforming lanes.
* **Risk Buffer Category:** Segment products into 'Critical', 'Standard', or 'Low-Risk' based on their average lead time volatility (Standard Deviation).



### Phase 3: Exploratory Data Analysis (The "What" and "When")

* **Task 3.1 (Univariate):** Create a **Box Plot** of `Lead_Time` grouped by `Disruption_Type`. This will visualize not just the average delay, but the "tail risk" or extreme outliers that cause supply chain shutdowns.
* **Task 3.2 (Time/Trend):** Build a **Line Chart** showing the `Monthly Average Delay` over the available time period. Use a **Rolling 3-Month Average** overlay to smooth out seasonal noise and identify if the supply chain is becoming more or less resilient over time.
* **Task 3.3 (Categorical):** Compare `Total Cost of Disruption` across different `Transportation_Modes` (Air, Sea, Rail, Road) using a **Grouped Bar Chart** to determine which mode is most vulnerable to external shocks.

### Phase 4: Advanced Analysis (The "Why" - Correlations & Patterns)

* **Task 4.1:** **Geospatial Risk Mapping:** Create a choropleth map or a bubble map showing `Disruption Frequency` by `Origin_Country` and `Destination_Country`.
* *Goal:* Identify "Choke Points"—specific geographic regions where disruptions are most frequent and costly.


* **Task 4.2:** **Supplier Segment Analysis:** Perform a **Quadrant Analysis** (Scatter Plot) comparing `Supplier_Lead_Time_Consistency` (X-axis) vs. `Unit_Cost` (Y-axis).
* *Goal:* Identify "High-Value/High-Risk" suppliers that require immediate diversification or alternative sourcing strategies.



---

## 4. Expected Deliverables & Output

Your final Jupyter Notebook must contain:

1. **Executive Summary:** A 3-point bulleted list of your biggest findings (e.g., "Air freight is 2x more prone to weather delays but 30% faster to recover than Sea freight").
2. **Clean Visualizations:** Every chart must have a `title`, `xlabel`, and `ylabel`. Use a professional color palette (e.g., `viridis` or `magma`).
3. **Business Logic:** Below each chart, add a Markdown cell answering: *"So what? How does this help the business?"*
4. **Final Recommendation:** A clear "Strategy Insight"—for instance, recommend a specific "Safety Stock" increase for the top 3 most disrupted routes identified.

---

## 💡 Pro-Tips & Suggestions

* **Performance:** Use `df.info(memory_usage='deep')` to monitor the size of your dataframe. For global datasets, converting categorical strings (like "Country" or "Mode") to the `category` dtype can significantly speed up your aggregations.
* **Aesthetics:** In Supply Chain reporting, **Red-Yellow-Green (Traffic Light)** color coding is standard. Use Red for high-risk disruption zones and Green for resilient routes to make your dashboard intuitive for executives.
* **The "Analyst Mindset":** Don't just report that a delay happened. Look for the **Recovery Time (Time to Recover - TTR)**. A supply chain that breaks often but fixes itself in 24 hours is often better than one that breaks once a year for three months.
