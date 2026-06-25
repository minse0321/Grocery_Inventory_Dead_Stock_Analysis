Grocery Inventory Dead Stock Analysis
Where is capital being locked up?
📌 Project Overview
In retail and food distribution, unsold inventory sitting in warehouses represents direct financial loss — tied-up capital that cannot be reinvested. This project investigates a core operational question:
Which product categories are accumulating dead stock, and how much capital is being locked up as a result?
Using a grocery inventory dataset of 989 products across 7 categories, this analysis identifies dead stock patterns by combining stock quantity, inventory turnover rate, and unit price data.

📂 Dataset
ItemDetailSourceKaggle — Grocery Inventory and Sales DatasetSize989 rows, 16 columnsNoteEducational dataset used for analytical demonstrationKey VariablesCategory, Stock_Quantity, Reorder_Level, Inventory_Turnover_Rate, Unit_Price, Status

🛠 Tech Stack
ToolUsagePython (Google Colab)Data cleaning, feature engineering, EDAPandasFiltering, groupby aggregationMatplotlib / SeabornExploratory visualizationsTableau PublicInteractive 4-chart dashboard

🔧 Data Cleaning & Preprocessing

Renamed typo column Catagory → Category
Converted Unit_Price from string ($4.50) to float
Parsed Date_Received, Last_Order_Date, Expiration_Date to datetime
Dropped 1 row with null Category → final shape (989, 16)
Date integrity issue: Expiration dates preceded received dates across most records — a data generation artifact. Date-based expiry analysis was excluded; analysis focused on stock quantity, turnover rate, and unit price instead.


⚙️ Feature Engineering
FeatureDefinitionDead_Stock_ScoreStock_Quantity × (1 / (Inventory_Turnover_Rate + 1))Is_Dead_StockTrue when Score ≥ 75th percentile AND Turnover ≤ 25th percentileTied_Up_ValueStock_Quantity × Unit_Price

📊 Dashboard
🔗 View on Tableau Public

🔍 Key Insights
1. Fruits & Vegetables has the most dead stock products

34 out of 192 dead stock products fall in this category — the highest volume of any category. High product count leads to proportionally higher inefficiency.
2. $74,918 in capital is locked up across dead stock products

Fruits & Vegetables accounts for $26,059 (35%) of total tied-up value. Beverages ranks 2nd at $12,237 despite having fewer dead stock products — driven by higher unit prices.
3. Dead stock clusters at low turnover rates

The scatter plot confirms that dead stock products (highlighted in red) concentrate in the low-turnover zone — products that move slowly tend to accumulate excess inventory.
4. Oils & Fats has the highest dead stock rate at 27.3%

Despite having fewer total products, more than 1 in 4 Oils & Fats products qualify as dead stock — the worst operational efficiency of any category.

💡 Strategic Recommendations
PriorityCategoryAction🔴 HighOils & FatsReduce reorder quantity; review supplier agreements🟠 MediumFruits & VegetablesTighten reorder triggers; monitor stock-to-sales ratio weekly🟡 LowBeveragesAudit high-value slow movers; consider promotional clearance

👤 Author
Minseo Choi · GitHub @minse0321

Business Administration, Gachon University

Aspiring Data Analyst | MSBA Candidate (Fall 2028)
