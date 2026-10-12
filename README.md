# Market Basket Analysis Using Association Rule Mining (Apriori)

**Student Name:** Kyeremateng Martin  
**Student Number:** 669217  
**Module:** DSA 4060A – Recommender Systems  
**Dataset:** `Groceries_dataset.csv` (38,765 transactional rows, 167 unique items)

---

## Project Overview
This repository contains a full end-to-end implementation of **Association Rule Mining** using the **Apriori Algorithm** to analyze retail purchasing behavior. The main objective is to discover hidden purchasing patterns, extract high-lift product bundles, and propose data-driven merchandising strategies to maximize retail sales.

## Key Methodology & Steps
1. **Data Loading & Cleaning**: Loaded the raw transactional dataset containing customer IDs, timestamps, and item descriptions.
2. **Exploratory Data Analysis (EDA)**: Visualized item distributions and identified the top 25 most frequently purchased items, led by `whole milk` (15.79%), `other vegetables` (12.21%), and `rolls/buns` (11%).
3. **Basket Reconstruction**: Grouped items by unique `Member_number` and `Date` combinations, resulting in **14,963 unique shopping baskets** with an average basket size of **2.59 items**.
4. **One-Hot Encoding**: Converted categorical baskets into a sparse binary matrix using `TransactionEncoder`.
5. **Frequent Itemset Mining (Apriori)**: Selected a sweet-spot minimum support threshold of `0.0005` (7-8 minimum occurrences) to discover **1,447 frequent itemsets**.
6. **Association Rule Generation & Refining**:
   - Generated an initial pool of rules at a low baseline confidence threshold (`min_confidence = 0.02`).
   - Refined the criteria to `min_confidence = 0.10` and `lift > 1.0` to filter out weak associations and noise, leaving **140 highly meaningful, actionable rules**.
7. **Visualization**: Created comprehensive scatter plots for Support vs. Confidence (mapped by Lift) and bar charts for top rules.

---

## Notable Insights & Rules
* **Top Association by Lift**: `{ham} ↔ {pickled vegetables}` (Lift: **~3.49**, Confidence: **~6.0%**). Buyers of ham are nearly 3.5 times more likely to purchase pickles than average.
* **Top Companion Fit**: `{soft cheese} ↔ {hamburger meat}` (Lift: **~2.75**).
* **Highest Probability / Confidence Rule**: `{sausage, pork} → {whole milk}`. When sausages and pork are co-purchased, there is a **39.1% chance** (Lift: **2.48**) the customer also picks up whole milk.

---

## Parameter Sensitivity & Support-Richness Trade-Off

| Minimum Support | Itemsets | Multi-Item Itemsets | Rules (conf ≥ 0.05, lift > 1) | Max Lift |
| :--- | :---: | :---: | :---: | :---: |
| 0.0100 | 69 | 5 | 0 | 0.000 |
| 0.0050 | 126 | 37 | 5 | 1.116 |
| 0.0010 | 750 | 601 | 94 | 2.183 |
| **0.0005** | **1,447** | **1,289** | **319** | **3.490** |
| 0.0003 | 2,393 | 2,230 | 975 | 14.704 |

*Selecting **0.0005** support successfully balances structural data richness with statistical reliability, ensuring rules are not based on accidental one-off transactions.*

---

## Repository Files
* **`DSA4060_Association_Mining_Rule.ipynb`**: The fully annotated, complete Jupyter Notebook containing all processing steps, visualizations, and markdown commentary.
* **`DSA4060_Association_Mining_Rule.html`**: A fully rendered, browser-ready HTML report generated directly from the notebook via `jupyter nbconvert` for static reading and grading.

## Setup and Execution
To replicate or run the notebook locally:
1. Ensure you have the required Python libraries installed:
   ```bash
   pip install pandas numpy matplotlib seaborn mlxtend
   ```
2. Put `Groceries_dataset.csv` in the same working directory.
3. Run all cells in `DSA4060_Association_Mining_Rule.ipynb` to regenerate the output tables, charts, and export the HTML report.
