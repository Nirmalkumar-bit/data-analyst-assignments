# 📝 Project: Predictive Workforce Resilience: Decoding Workload & Attrition

## 1. Project Overview

**Role:** People Analytics Consultant

**Objective:** Identify the critical tipping points where employee workload leads to burnout and attrition. The goal is to provide HR leadership with a data-driven "Early Warning System" to reduce turnover costs and optimize departmental resource allocation.

---

## 2. Resources & Links

* **Dataset Source:** [Employee Workload and Attrition Analysis](https://www.kaggle.com/datasets/jayjoshi37/employee-workload-and-attrition-analysis)
* **Target Files:** `employee_data.csv` (Primary dataset containing demographics, satisfaction, and workload metrics)
* **Documentation/Tools:** * **Specific Library:** `Seaborn` for advanced statistical data visualization.
* [Seaborn Statistical Categorical Plotting Documentation](https://seaborn.pydata.org/tutorial/categorical.html)



---

## 3. Detailed Task Instructions

### Phase 1: Ingestion & Data Quality Audit (The Foundation)

* **Task 1.1:** Load the dataset using Pandas. Since this is a structured CSV, ensure you check the initial `info()` to verify if data types (specifically integers vs. floats) align with the column descriptions.
* **Task 1.2:** Audit the **Satisfaction Levels** and **Workload Metrics**. Check for "Out of Bounds" errors (e.g., satisfaction scores greater than 1.0 or negative hours worked) and verify the consistency of the 'Left' (Attrition) column.
* **Task 1.3:** Handle missing values. Given that employee records are sensitive, determine if nulls should be imputed using the median (to avoid outlier skew) or if the rows should be dropped to maintain data integrity for predictive modeling.

### Phase 2: Feature Engineering (The Senior Analyst Step)

* **Task 2.1:** Create 3 new metrics to quantify "Burnout Risk":
* **Workload Intensity:** Create a ratio of `Average_Monthly_Hours` divided by `Number_of_Projects`.
* **Tenure Milestone:** Categorize `Time_Spend_Company` into 'New Hire' (0-2y), 'Established' (3-5y), and 'Veteran' (6y+).
* **Overachiever Flag:** A Boolean column identifying employees with high evaluation scores but low satisfaction (a high-risk attrition group).



### Phase 3: Exploratory Data Analysis (The "What" and "When")

* **Task 3.1 (Univariate):** Create a **Kernel Density Estimate (KDE) Plot** of `Satisfaction_Level`. Compare the distribution of employees who stayed vs. those who left to find the "Danger Zone" score.
* **Task 3.2 (Categorical/Workload):** Visualize the relationship between the `Number_of_Projects` and `Average_Monthly_Hours` using a **Box Plot**, segmented by `Left`.
* **Task 3.3 (Group Comparison):** Use a **Stacked Bar Chart** to compare Attrition Rates across different `Departments`. Which department is the "Leaky Bucket"?

### Phase 4: Advanced Analysis (The "Why" - Correlations & Patterns)

* **Task 4.1 (Correlation Heatmap):** Generate a Pearson Correlation Heatmap specifically looking for the relationship between `Work_Accident`, `Promotion_Last_5_Years`, and `Left`.
* *Goal:* Determine if career stagnation (lack of promotion) is a stronger predictor of attrition than physical workload.


* **Task 4.2 (Segmentation):** Perform a "Burnout Quadrant" analysis. Group employees into four clusters based on `Evaluation` (High/Low) and `Satisfaction` (High/Low). Identify the "Stars at Risk"—those with high performance but low satisfaction.

---

## 4. Expected Deliverables & Output

Your final Jupyter Notebook must contain:

1. **Executive Summary:** A 3-point bulleted list highlighting the top 3 drivers of attrition (e.g., "Employees with >5 projects see a 40% spike in turnover").
2. **Clean Visualizations:** Every chart must use a professional color palette (e.g., `viridis` or `RdBu`) and include a `title`, `xlabel`, and `ylabel`.
3. **Business Logic:** Below each chart, add a Markdown cell answering: *"So what? How does this help the HR Director decide which department needs a budget increase or a headcount hire?"*
4. **Final Recommendation:** A specific "Retention Strategy" (e.g., "Implement a project cap of 4 for employees in the Technical department").

---

## 💡 Pro-Tips & Suggestions

* **Performance:** Use `.astype('category')` for columns like 'Department' and 'Salary' to save memory and speed up plotting functions.
* **Aesthetics:** Use `sns.despine()` to remove unnecessary borders from your charts, giving them a modern, "McKinsey-style" look.
* **The "Analyst Mindset":** In HR data, "No Correlation" is often a finding in itself. If high salary doesn't stop people from leaving, the problem is likely culture or workload—focus your story there.

---