# E-commerce Return Analysis & Prediction

This end-to-end data analysis project investigates the drivers of e-commerce product returns. It moves from data preparation (SQL) and predictive modeling (Python) to a final interactive dashboard (Tableau).

The core of this project is to not only diagnose *why* returns happened in the past, but to build a machine learning model that predicts *which* items are at high risk of being returned in the future.

## 🔗 Live Interactive Dashboard

The final 3-page dashboard is hosted on Tableau Public. Click the link below to interact with the visualizations.

**[Live Dashboard: E-commerce Return Analysis](https://public.tableau.com/app/profile/aaryan.raj2569/viz/E-commerceReturnAnalysis/1_ExecutiveOverview?publish=yes)**

---

## 🛠️ Tools & Stack

* **Database:** MS SQL Server (for initial data import and joining)
* **Data Analysis:** Python (Pandas, Matplotlib, Seaborn)
* **Machine Learning:** Python (Scikit-learn)
* **Data Visualization:** Tableau

---

## 📈 Project Workflow

### 1. Database & ETL
* Imported raw `Orders.csv` and `Returns.csv` files into a local MS SQL Server database.
* Wrote a `LEFT JOIN` query to merge the two tables and create a master dataset. A `CASE` statement was used to create a new `Is_Returned` flag (1 for returned, 0 for not returned).

### 2. Diagnostic Analysis (Python)
* Loaded the merged data into a Google Colab notebook (`Return_Analysis.ipynb`).
* Performed exploratory data analysis (EDA) to find the "why" behind returns.
* **Key Insight 1:** Identified that the **"Tables" sub-category** was a major problem, having one of the highest return rates.
* **Key Insight 2:** Analyzed `Region` and `Discount` to find that high-discount items were not necessarily correlated with higher returns, but certain regions had significantly worse performance.

### 3. Predictive Modeling (Python)
* Built a **Logistic Regression** model (using Scikit-learn) to predict the probability of an item being returned.
* **Crucial Challenge:** The dataset was **highly imbalanced** (over 95% of items were not returned). A basic model would achieve 95% accuracy by simply guessing "no return" every time, making it useless.
* **Solution:** I addressed this by setting the `class_weight='balanced'` parameter in the model. This technique forces the model to pay much more attention to the minority class (the returns), allowing it to learn the *actual* patterns that lead to a return.
* **Result:** The final, balanced model generated a `Return_Risk_Score` (a probability from 0 to 1) for all 51,000+ items in the catalog.

### 4. Interactive Dashboard (Tableau)
* Loaded the final dataset, now including the `Return_Risk_Score`, into Tableau.
* Created the `E-commerce Return Analysis.twbx` workbook with three main dashboard pages:
    * **Page 1: Executive Overview:** A high-level summary of KPIs, a map of problem regions, and top-level category return rates.
    * **Page 2: Root Cause Analysis:** Interactive charts to drill down into *why* returns happen, including a scatter plot of `Profit vs. Return Rate` to find the most damaging products.
    * **Page 3: Risk Forecast:** A filterable, sortable list of the highest-risk products, using the `Return_Risk_Score` from our Python model. This allows a manager to proactively manage inventory and prevent future losses.

---

## 📂 Repository Contents

* `Return_Analysis.ipynb`: The Google Colab notebook containing all Python analysis, data cleaning, and Scikit-learn modeling.
* `E-commerce Return Analysis.twbx`: The Tableau Packaged Workbook. This file can be downloaded and opened in Tableau Desktop to view and interact with the final dashboard.
* `tableau_data.csv`: The final, cleaned dataset output from Python (includes the `Return_Risk_Score`) and used as the source for the Tableau dashboard.
* `high_risk_products.csv`: A deliverable list of the top 100 high-risk products, as predicted by the machine learning model.
