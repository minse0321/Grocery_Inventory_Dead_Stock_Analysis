# 📦 Grocery Inventory Dead-Stock Analysis: Where Is Capital Getting Stuck?

## Why I did this

I studied trade, logistics, and distribution at Halla University before moving into Business Administration. Inventory is the part of logistics that shows up most directly in money: stock that doesn't sell just sits in a warehouse, and the cash tied up in it can't be used for anything else.

I wanted a project where I define the problem myself instead of following a tutorial. That meant deciding what "dead stock" means, flagging it, and putting a dollar figure on it.

The dataset is for educational use, and some of its fields are clearly generated (see Limitations). I used it to practice the method, so I'm not treating the numbers as a real company's.

## The question

**Which product categories are accumulating dead stock, and how much capital is tied up in it?**

## What I found

| | Finding |
|---|---|
| 📦 | **192 of 989 products** were flagged as dead stock under my definition (see below) |
| 💰 | Those products hold **$74,918** in tied-up value (stock quantity × unit price) |
| 🥬 | Fruits & Vegetables has the most dead-stock products (34 of the 192) and the largest tied-up value ($26,059, 35% of the total) |
| 🥫 | Oils & Fats has the highest dead-stock **rate** at 27.3%, so more than 1 in 4 of its products is stuck |
| 🥤 | Beverages is second in tied-up value ($12,237) with fewer dead-stock products, because their unit prices are higher |

## How I defined dead stock

| Feature | Definition |
|---|---|
| `Dead_Stock_Score` | Stock_Quantity × (1 / (Inventory_Turnover_Rate + 1)) |
| `Is_Dead_Stock` | True when the score is in the top 25% **and** turnover is in the bottom 25% |
| `Tied_Up_Value` | Stock_Quantity × Unit_Price |

The score and the cutoffs are my own choices, not an industry standard. That means the number 192 depends on them. Also, since the definition uses turnover, dead-stock products naturally sit in the low-turnover zone. That is by construction, not a finding.

## Why it matters for a business

Money stuck in slow stock can't be spent on faster-moving items, and in a food business it also means storage cost and spoilage risk. The three categories have different problems:

- **Oils & Fats** is a *rate* problem: a large share of its products is stuck
- **Fruits & Vegetables** is a *size* problem: it holds the most capital
- **Beverages** is a *price* problem: few products, but expensive ones

These are proposals, not tested results.

| Priority | Category | Suggested action | How I'd check it works |
|---|---|---|---|
| 🔴 High | Oils & Fats | Reduce reorder quantity; review supplier agreements | Compare turnover and dead-stock rate before and after |
| 🟠 Medium | Fruits & Vegetables | Tighten reorder triggers; track the stock-to-sales ratio weekly | See whether tied-up value falls over the next few reorder cycles |
| 🟡 Low | Beverages | Audit high-value slow movers; consider promotional clearance | Compare the clearance margin to the cost of holding the stock |

I ranked by how widespread the problem is (the rate). Ranking by dollar value would put Fruits & Vegetables first.

## Limitations and next steps

- **Generated data.** Expiration dates came before received dates in most records, so I dropped expiry analysis. This also means perishability, the obvious risk for fruit and vegetables, isn't captured
- **My own definition.** The count of 192 depends on the 75th/25th percentile cutoffs. **Next:** try other cutoffs (for example 70/30 and 80/20) and check whether the category ranking holds
- **"Capital" is approximate.** I multiplied stock by unit price, which is probably a selling price rather than a cost, so the figure may overstate what is actually tied up
- **Descriptive only.** No statistical tests here. **Next:** compare categories formally instead of just ranking them
- **Stock vs sales.** I flagged slow movers by turnover only. **Next:** use sales volume to calculate days of stock on hand, and add an ABC classification by value

## Data cleaning

- Renamed the typo column `Catagory` to `Category`
- Converted `Unit_Price` from string (`$4.50`) to float
- Parsed `Date_Received`, `Last_Order_Date`, `Expiration_Date` to datetime
- Dropped 1 row with a null Category, so the final shape is (989, 16)

## Tech stack

| Tool | Usage |
|---|---|
| Python (Google Colab) | Cleaning, feature engineering, EDA |
| pandas | Filtering, groupby aggregation |
| Matplotlib | Exploratory charts |
| Tableau Public | Interactive 4-chart dashboard |

## Dataset

| Item | Detail |
|---|---|
| Source | Kaggle, Grocery Inventory and Sales Dataset |
| Size | 989 rows, 16 columns (after cleaning) |
| Note | Educational dataset |
| Key variables | Category, Stock_Quantity, Reorder_Level, Inventory_Turnover_Rate, Unit_Price, Status |

## Dashboard

🔗 [View on Tableau Public](https://public.tableau.com/app/profile/minseo.choi4768/viz/GroceryInventoryDeadStockAnalysis/GroceryInventoryDeadStockAnalysis)

## Repository structure

grocery-inventory-dead-stock-analysis/
├── README.md
├── Grocery_Inventory_Dead_Stock_Analysis.ipynb
└── data/
    ├── grocery_cleaned.csv
    └── dead_stock_products.csv
