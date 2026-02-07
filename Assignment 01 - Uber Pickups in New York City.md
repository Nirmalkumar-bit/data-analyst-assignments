# 📝 Project: Urban Pulse: Optimizing Fleet Allocation via Spatiotemporal Analysis

## 1. Project Overview

**Role:** Fleet Operations Analyst

**Objective:** Analyze six months of Uber pickup data in New York City to identify high-demand "hotspots" and peak time windows, enabling the operations team to proactively position drivers and reduce customer wait times.

---

## 2. Resources & Links

* **Dataset Source:** [Kaggle: Uber Pickups in New York City](https://www.kaggle.com/datasets/fivethirtyeight/uber-pickups-in-new-york-city)
* **Target Files:** `uber-raw-data-apr14.csv` through `uber-raw-data-sep14.csv` (The monthly raw pickup files).
* **Documentation/Tools:** * **Folium:** A powerful Python library for visualizing geospatial data.
* [Folium Documentation](https://python-visualization.github.io/folium/)



---

## 3. Detailed Task Instructions

### Phase 1: Ingestion & Data Quality Audit (The Foundation)

* **Task 1.1:** Write a script to loop through and concatenate the six separate monthly CSV files (April through September) into a single DataFrame. Ensure the `Date/Time` column is parsed correctly as a datetime object, not a string.
* **Task 1.2:** Perform a "Geospatial Sanity Check." New York City fits roughly within Latitudes 40.5° to 40.9° and Longitudes -74.25° to -73.7°. Identify and remove any rows where coordinates fall significantly outside this bounding box (GPS errors).
* **Task 1.3:** Check for duplicate timestamp/location pairs. In high-frequency transactional data, system glitches can record a single pickup twice.

### Phase 2: Feature Engineering (The Senior Analyst Step)

* **Task 2.1:** Deconstruct the `Date/Time` column into granularity that drives business decisions:
* `Hour` (0-23)
* `Day_of_Week_Name` (Monday-Sunday)
* `Month`


* **Task 2.2:** Create a `Rush_Hour` flag (Binary 1/0). Define this based on standard NYC traffic patterns (e.g., 7-9 AM and 4-7 PM on weekdays).
* **Task 2.3:** Categorize `Base` codes into readable company names if external mapping is available, or simply encode them as categorical variables for performance.

### Phase 3: Exploratory Data Analysis (The "What" and "When")

* **Task 3.1 (Univariate - Temporal):** Create a Histogram of total pickups by `Hour`. Identify the absolute peak demand hour and the lowest demand hour.
* **Task 3.2 (Time/Trend - Weekly):** Visualize the "Weekly Rhythm." Create a line or bar chart showing Total Pickups by `Day_of_Week`. Does demand spike on Fridays/Saturdays?
* **Task 3.3 (Categorical - Base Analysis):** Compare the volume of pickups across the different dispatching bases (B02512, B02598, etc.). Use a Bar Chart to see if one base dominates the market share.

### Phase 4: Advanced Analysis (The "Why" - Correlations & Patterns)

* **Task 4.1 (Geospatial Analysis):** Generate an interactive Heatmap using Folium (or Plotly) plotted on a map of NYC.
* *Goal:* Visually confirm if demand is centralized in Manhattan or dispersed across boroughs like Brooklyn and Queens.


* **Task 4.2 (Clustering/Segmentation):** Use **K-Means Clustering** based on Longitude and Latitude to create distinct "Demand Zones."
* *Goal:* Instead of infinite coordinates, group the city into 5-10 logical operating clusters to simplify driver assignment instructions.



---

## 4. Expected Deliverables & Output

Your final Jupyter Notebook must contain:

1. **Executive Summary:** A 3-point bulleted list of your biggest findings at the very top of the file (e.g., "Demand peaks at 5 PM," "Manhattan accounts for 70% of trips").
2. **Clean Visualizations:** Every chart must have a `title`, `xlabel`, and `ylabel`.
3. **Business Logic:** Below each chart, add a Markdown cell answering: *"So what? How does this help the business?"* (e.g., "Because demand peaks at 5 PM, we should incentivize drivers to log on at 4:30 PM.")
4. **Final Recommendation:** A clear "Strategy Insight" proposing a shift schedule or location strategy for drivers.

---

## 💡 Pro-Tips & Suggestions

* **Performance:** This dataset contains millions of rows. If your visualizations are slow, consider down-sampling your data (e.g., taking a random 10% sample) for the development of your Heatmaps, then run the full set for the final export.
* **Aesthetics:** Use a dark theme (like `plotly_dark` or `folium.Map(tiles='CartoDB dark_matter')`) for maps; it makes the data points/heatmaps pop significantly more than standard light maps.
* **The "Analyst Mindset":** Remember, a car cannot be everywhere at once. Your goal is not just to show *where* cars are needed, but *when* they are needed there. The interaction between Time and Location is where the value lies.