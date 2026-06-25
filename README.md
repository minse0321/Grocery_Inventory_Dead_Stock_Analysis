# Grocery Inventory Dead Stock Analysis
**Where is capital being locked up?**

## 📌 Project Overview
In retail and food distribution, unsold inventory sitting in warehouses represents direct financial loss — tied-up capital that cannot be reinvested. This project investigates a core operational question:

*Which product categories are accumulating dead stock, and how much capital is being locked up as a result?*

Using a grocery inventory dataset of 989 products across 7 categories, this analysis identifies dead stock patterns by combining stock quantity, inventory turnover rate, and unit price data.

---

## 📂 Dataset
| Item | Detail |
|---|---|
| Source | Kaggle — Grocery Inventory and Sales Dataset |
| Size | 989 rows, 16 columns |
| Note | Educational dataset used for analytical demonstration |
| Key Variables | Category, Stock_Quantity, Reorder_Level, Inventory_Turnover_Rate, Unit_Price, Status |

---

## 🛠 Tech Stack
| Tool | Usage |
|---|---|
| Python (Google Colab) | Data cleaning, feature engineering, EDA |
| Pandas | Filtering, groupby aggregation |
| Matplotlib / Seaborn | Exploratory visualizations |
| Tableau Public | Interactive 4-chart dashboard |

---

## 🔧 Data Cleaning & Preprocessing
- Renamed typo column `Catagory` → `Category`
- Converted `Unit_Price` from string (`$4.50`) to float
- Parsed `Date_Received`, `Last_Order_Date`, `Expiration_Date` to datetime
- Dropped 1 row with null Category → final shape (989, 16)
- **Date integrity issue**: Expiration dates preceded received dates across most records — a data generation artifact. Date-based expiry analysis was excluded; analysis focused on stock quantity, turnover rate, and unit price instead.

---

## ⚙️ Feature Engineering
| Feature | Definition |
|---|---|
| `Dead_Stock_Score` | Stock_Quantity × (1 / (Inventory_Turnover_Rate + 1)) |
| `Is_Dead_Stock` | True when Score ≥ 75th percentile AND Turnover ≤ 25th percentile |
| `Tied_Up_Value` | Stock_Quantity × Unit_Price |

---

## 📊 Dashboard
🔗 [View on Tableau Public](https://public.tableau.com/app/profile/minseo.choi4768/viz/GroceryInventoryDeadStockAnalysis/GroceryInventoryDeadStockAnalysis)

---

## 🔍 Key Insights

**1. Fruits & Vegetables has the most dead stock products**
34 out of 192 dead stock products fall in this category. High product count leads to proportionally higher inefficiency.

**2. $74,918 in capital is locked up across dead stock products**
Fruits & Vegetables accounts for $26,059 (35%) of total tied-up value. Beverages ranks 2nd at $12,237 despite fewer dead stock products — driven by higher unit prices.

**3. Dead stock clusters at low turnover rates**
The scatter plot confirms dead stock products concentrate in the low-turnover zone — products that move slowly tend to accumulate excess inventory.

**4. Oils & Fats has the highest dead stock rate at 27.3%**
More than 1 in 4 Oils & Fats products qualify as dead stock — the worst operational efficiency of any category.

---

## 💡 Strategic Recommendations
| Priority | Category | Action |
|---|---|---|
| 🔴 High | Oils & Fats | Reduce reorder quantity; review supplier agreements |
| 🟠 Medium | Fruits & Vegetables | Tighten reorder triggers; monitor stock-to-sales ratio weekly |
| 🟡 Low | Beverages | Audit high-value slow movers; consider promotional clearance |

---

## 📁 Repository Structure
grocery-inventory-dead-stock-analysis/

├── README.md

├── Grocery_Inventory_Dead_Stock_Analysis.ipynb

└── data/

├── grocery_cleaned.csv

└── dead_stock_products.csv
---
