# E-commerce Return Analysis & Prediction

This project analyzes a global e-commerce dataset to identify the key drivers of product returns and builds a machine learning model to predict future return risk.

The analysis moves from data preparation in SQL, to diagnostic analysis and predictive modeling in Python, culminating in a 3-page interactive dashboard in Tableau for business users.

## 🔗 Live Interactive Dashboard

The final 3-page dashboard is hosted on Tableau Public. Click the link below to interact with the visualizations.

**[Live Dashboard: E-commerce Return Analysis](https://public.tableau.com/app/profile/aaryan.raj2569/viz/E-commerceReturnAnalysis/1_ExecutiveOverview?publish=yes)**

![Dashboard Screenshot](dashboard_screenshot.png)

---

## 🛠️ Tools & Stack

* **Database:** MS SQL Server (for initial data import and joining)
* **Data Analysis:** Python (Pandas, Matplotlib, Seaborn)
* **Machine Learning:** Python (Scikit-learn)
* **Data Visualization:** Tableau

---

## 📈 Project Phases

### 1. Database & ETL
* Imported raw `Orders.csv` and `Returns.csv` files into a local MS SQL Server database.
* Wrote a SQL query using a `LEFT JOIN` and `CASE` statement to create a master dataset, flagging all returned items with an `Is_Returned` column.

### 2. Diagnostic Analysis (The "Why")
* Loaded the merged dataset into a Google Colab notebook.
* Performed exploratory data analysis (EDA) to find patterns.
* **Key Insight 1:** Analyzed return rates by `Category` and `Sub-Category`, identifying which product lines are the most problematic.
* **Key Insight 2:** Investigated `Region` and `Country` data to pinpoint geographic hotspots for returns.
* **Key Insight 3:** Plotted `Return Rate` against `Discount` to see if sales promotions were driving costly returns.

### 3. Predictive Modeling (The "What's Next")
* **Problem:** The dataset was highly imbalanced (over 95% of items were not returned). A basic model would be 95% accurate by simply guessing "0" (no return).
* **Solution:** Built a **Logistic Regression** model using `class_weight='balanced'`. This technique penalizes the model for misclassifying the minority class (the returns), forcing it to learn the *actual* patterns of problem items.
* **Result:** Created a `Return_Risk_Score` (a probability from 0 to 1) for every item in the catalog.

### 4. Interactive Dashboard
* Loaded the final dataset (including the `Return_Risk_Score`) into Tableau.
* **Page 1: Executive Overview:** A high-level summary of KPIs, a map of problem regions, and top-level category return rates.
* **Page 2: Root Cause Analysis:** Interactive charts to drill down into *why* returns happen, including a scatter plot of `Profit vs. Return Rate` to find the most damaging products.
* **Page 3: Risk Forecast:** A sortable, filterable list of the highest-risk products, allowing a manager to proactively manage inventory and prevent future losses.

---

## 📂 Repository Contents

* `Return_Analysis.ipynb`: The Google Colab notebook with all Python analysis and Scikit-learn modeling.
* `tableau_data.csv`: The final, cleaned dataset used for the Tableau dashboard (includes risk scores).
* `high_risk_products.csv`: A deliverable list of the top 100 products most likely to be returned, as predicted by the model.
* `dashboard_screenshot.png`: A screenshot of the main dashboard.
