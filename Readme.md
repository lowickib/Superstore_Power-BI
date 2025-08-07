# 🚀 Power BI Retail Analytics Dashboard – Superstore Project

![Dashboard demo](imgs/GIF/Superstore%20Demo.gif)

📎 [**View Interactive Dashboard**](https://app.powerbi.com/view?r=eyJrIjoiMGZiMWVjMTgtMmM3MS00ODRiLTk2MjQtYzg2OTQyY2Y1YTgxIiwidCI6IjY0YmU5OWY5LTI2N2MtNDIxMS1iMDlhLTQ0YmZlNjYyMzY0MCJ9)

---

## 🧠 Project Summary & Skills Showcased

This end-to-end Power BI project showcases my expertise in **data modeling**, **DAX**, and **dashboard design** using a fictional retail dataset from Kaggle.  
It simulates a real-world analytics solution for **sales, product, customer, and geographic performance monitoring**, highlighting actionable business insights and visual storytelling best practices.

---

### 🔧 Tools, Techniques & Technologies
- **Power Query ETL**: Star schema, calendar dimension, fact/dim tables
- **DAX**: Advanced logic (Top N by hierarchy, YoY %, dynamic targets, slicer-dependent titles)
- **UX/UI**: Custom slicer panel, KPI toggle, drillthroughs, bookmarks, conditional formatting
- **Customer Segmentation**: RFM model with dynamic tooltips
- **Performance Optimization**: Star schema, no calculated columns, reusable measures

---

### 📊 Report Features
- **6 report pages + 2 drillthroughs**, including:
  - Executive summary
  - Time trends & targets
  - Product & category performance
  - Customer insights & RFM segmentation
  - Territory analysis
- **Dynamic KPI toggle** (Orders / Sales / Profit) across all main pages
- **Adaptive KPI targets** based on trailing 3-month averages (+10% growth)
- **Top N logic** responsive to slicers & hierarchy levels (city/state/product)
- **Custom tooltips**: RFM distribution, top product details, filtered insights

---

### 📌 Business Value & Insights
- Identifies **top-performing products, regions, and customer segments**
- Highlights **unprofitable regions** despite high sales (e.g. Texas, Florida)
- Enables **target vs. actual performance** tracking with adaptive benchmarks
- Supports decisions on **marketing**, **inventory optimization**, and **customer retention**

---

### 💡 Key Learnings
- Wrote complex DAX logic using `ISINSCOPE`, `TOPN`, `KEEPFILTERS`, and `RANKX`
- Created **bookmark-driven KPI toggles** and **custom tooltip pages**
- Solved **Top N by hierarchy level** with community support  
  [See solution](https://community.fabric.microsoft.com/t5/Desktop/Filter-top-N-elements-on-both-levels-of-hierarchy/m-p/4789542#M1426101)
- Optimized performance through model simplification and reuse of measures

---

### 🧠 Skill Areas Demonstrated

#### 🔧 Data Preparation & Modeling
- Power Query for filtering, transformation, and normalization
- Star schema design with fact and dimension tables
- Calendar table with full time intelligence
- Surrogate keys for RFM segmentation (1:1 relationship)

#### 📊 DAX Calculations
- 80+ reusable measures: Sales, Orders, Profit, Time Trends, RFM, UX logic
- Advanced DAX using: `SWITCH`, `SELECTEDVALUE`, `TOPN`, `ISINSCOPE`, `KEEPFILTERS`
- Rolling averages, YoY%, targets, and dynamic titles
- Top N logic adjusting to slicer values and hierarchy level

#### 📈 Data Visualization & Storytelling
- Multi-page dashboard with diverse chart types: area, ribbon, scatter, treemap, donut, bar
- Custom tooltips and label tricks for clearer storytelling
- Drillthrough pages for deep-dive into products and customer segments

#### 🎨 UX/UI Design
- Unified layout with consistent placement of KPIs and filters
- Bookmark-driven navigation and slicer panel
- Dynamic filter indicator icon with tooltip (white/yellow)
- Toggle switcher for KPIs to avoid chart duplication

#### 📦 Business Analysis & Interpretation
- RFM-based customer segmentation and analysis
- Comparison of Total vs. Average metrics across segments
- Detection of seasonal trends and underperforming regions
- Actionable insight generation for real business scenarios


## 📊 Data Source

The dataset used in this project comes from a publicly available source on Kaggle:

**Link:**  
[Superstore Dataset (Final) – Kaggle](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final/data)

This dataset contains over 9,900 rows of fictional retail sales data covering the years **2014–2017**. It is commonly used to practice business analysis, customer segmentation, and KPI visualization.

**Main file:**

- `Sample - Superstore.csv` – the primary dataset file, including:
  - **Order details** – Order ID, Order Date, Ship Date, Ship Mode
  - **Customer information** – Customer ID, Segment, Region
  - **Product details** – Product Name, Category, Sub-Category
  - **Sales metrics** – Sales, Quantity, Discount, Profit

## 🎯 Business Objectives

This dashboard was designed to support **data-driven decision making** across sales, product, customer, and geographic performance.  
It aims to answer the following **key business questions**:

### 🛒 Sales & Product Performance
- Which **products** generate the most **sales**, **orders**, and **profit**?
- What are the **top-performing categories and sub-categories** over time?
- How does performance **fluctuate seasonally** or by **day of the week**?
- Which **products are underperforming** and may require promotional actions or delisting?

### 👥 Customer Insights & Segmentation
- How are customers distributed across **RFM segments**?
- What is the **average order value**, **frequency**, and **recency** by segment?
- Which customer segments contribute most to **profitability**?
- How do customer behaviors differ across segments like "Loyal & Valuable" vs. "At Risk"?

### 🌍 Regional & Geographic Analysis
- Which **states or cities** drive the most **revenue and profit**?
- Are there **regions with negative profit** that require strategic review?
- What are the **top-performing territories**, and how do they compare?

### 🎯 Drill-through & Detail-Level Exploration
- What are the **monthly trends** for a specific **product** or **RFM segment**?
- Which **geographic regions** or **product categories** are linked to a given segment’s behavior?
- How do **profit and sales performance** break down over time for individual selections?

---

These objectives shape the dashboard structure, interactivity, and KPI definitions to ensure each page contributes to solving real-world business challenges.


## 🔄 Data Preparation (Power Query ETL)

The original dataset (`Sample - Superstore.csv`) was imported and transformed using **Power Query**. The file was split into multiple fact and dimension tables to follow a **star schema** structure in Power BI.

### 🧾 Tables created from the source file:

#### **FactSales**
Contains core transactional metrics:
- Row ID, Order ID, Product ID
- Sales, Quantity, Discount, Profit

#### **DimOrders**
Stores order-specific metadata:
- Order ID, Order Date, Ship Date, Ship Mode
- Customer ID, Postal Code

> This table was **intentionally separated from FactSales** because order-related information (such as dates, customer, shipping mode) was **repeated for every product in the same order** in the original dataset. Separating this data helps reduce redundancy and supports better normalization.

#### **DimProducts**
Describes products and their hierarchy:
- Product ID, Product Name
- Category, Sub-Category

> Further normalization by extracting **Category** and **Sub-Category** into separate dimension tables was considered, but not implemented. This is due to **Power BI Service limitations** — particularly, **join operations between datasets are only available with a Premium Capacity license**. To ensure compatibility with **Power BI Pro**, the structure was kept simpler.

#### **DimCustomers**
Includes basic customer details:
- Customer ID, Customer Name, Segment

#### **DimTerritory**
Captures geographic and regional data:
- Postal Code, City, State, Region, Country

#### **DimCalendar**
A dynamic date dimension table was created using the range of order dates found in the dataset. It includes columns such as:
- Year, Month, Month Name
- Quarter, Day Name, Day of Week, Week of Year, etc.

---

## 📈 RFM Table (Customer Segmentation)

An additional table was created for **RFM (Recency–Frequency–Monetary)** analysis. This is not a traditional dimension table, but an **analytical layer** used for customer segmentation.

### Key fields and logic:
- **Recency**: Days since last order
- **Frequency**: Number of unique orders
- **Monetary**: Total spending per customer

Each metric was ranked and scored (0–10 scale), and a **combined RFM score** was computed. Based on that, customers were assigned to the following segments:

| RFM Score Range | Segment              |
|------------------|-----------------------|
| 9–10             | Top Customer          |
| 7–8              | Loyal & Valuable      |
| 5–6              | Promising / Average   |
| 3–4              | At Risk / Sleeping    |
| 0–2              | Churned / Inactive    |

A numerical field `Customer Segment Order` was also created to control the logical order of segments in visuals.

## 🧩 Data Model & Relationships

The data model follows a **star schema** structure, with one central fact table (**FactSales**) and several supporting dimension tables. 

### 🔗 Defined relationships:

| From Table (Column)         | To Table (Column)               | Type             | Status  |
|-----------------------------|----------------------------------|------------------|---------|
| DimOrders (Customer ID)     | DimCustomers (Customer ID)      | Many-to-One (*)  | Active  |
| DimOrders (Order Date)      | DimCalendar (Date)              | Many-to-One (*)  | Active  |
| DimOrders (Postal Code)     | DimTerritory (Postal Code)      | Many-to-One (*)  | Active  |
| FactSales (Order ID)        | DimOrders (Order ID)            | Many-to-One (*)  | Active  |
| FactSales (Product ID)      | DimProducts (Product ID)        | Many-to-One (*)  | Active  |
| RFM (Customer ID)           | DimCustomers (Customer ID)      | One-to-One (1:1) | Active  |

### 💡 Notes:
- All relationships use **single-directional filtering** (`* -> 1`).
- The `RFM` table is linked using a **1:1 relationship** to `DimCustomers`, as each customer has a unique RFM profile.
- The model is optimized for **readability, reusability, and performance**, aligning with best practices in dimensional modeling.

## 📊 Page 1 – Executive Summary
![Page 1 – Executive Summary](imgs/PNGs/1%20-%20Overview.png)
This landing page provides a **high-level overview** of business performance, highlighting overall trends and top contributors based on the selected KPI (Orders, Profit, or Sales).

### 🔹 Key Components

#### ✅ KPI Summary Cards (Top)
- **Total Orders**
- **Total Profit**
- **Total Sales**  
These cards are **static and independent** of the dynamic toggle button.  
Each card always displays its respective metric, providing a consistent snapshot of core business performance regardless of selected measure elsewhere on the page.


#### 📉 KPI Trend by Month
- **Dynamic line and area chart** showing:
  - `Total Orders / Profit / Sales by Month`
- Includes:
  - Interactive date slider
  - Trendline
- Helps track long-term performance and seasonality.

#### 🗂️ Selected Measure by Category and Subcategory
- **Treemap chart** displaying the **Selected Measure** (`Total Orders`, `Total Profit`, or `Total Sales`) by **Category** and **Subcategory**
- Visual uses a **drillable hierarchy** (Category → Subcategory)
- Size and color represent values, helping quickly identify:
  - Leading and underperforming product groups
  - Relative contribution of subcategories within each category


#### 🎯 Monthly KPI Targets (Bottom Row)

Three dynamic KPI cards:
1. **Monthly Orders**
2. **Monthly Profit**
3. **Monthly Sales**

Each tile displays:
- **Current month's value**
- **Projected target**: +10% growth over the recent 3-month average
- **% Difference vs. target**: 
  - Color-coded to indicate underperformance or exceeding the goal
  - Dynamically changes as new data is loaded

These cards help monitor real-time performance against adaptive benchmarks, with automatic month-over-month updates.


#### 🏆 Top Products by KPI
- **Table listing the Top 25 Products** by selected measure:
  - Product ID
  - Product Name
  - Total Orders
  - Total Profit
  - Total Sales
  - Rank  
- Powered by **dynamic Top N logic**, adapting to user-selected KPI.

---

### 🎯 Purpose of the Page

This page is designed for:
- Executives and managers who need

## 📄 Page 2 – Time Intelligence Analysis
![Page 2 – Time Intelligence Analysis](imgs/PNGs/2%20-%20Time%20Trends.png)
This page focuses on temporal analysis across multiple time granularities (year, month, week), helping stakeholders understand trends, seasonality, and performance dynamics over time.

### ✅ % Year-over-Year Change Cards (Top Right)
Three static KPI cards display **YoY growth** (compared to the same month last year) for:
- `% YoY Orders Change`
- `% YoY Profit Change`
- `% YoY Sales Change`

These indicators provide high-level trend insights and help evaluate performance momentum.

---

### 📈 Selected Measure YTD (Top Left)
- **Area chart** showing `Selected Measure YTD` (Year-To-Date) across multiple years.
- Uses color-coded lines per year (2014–2017) to compare cumulative performance over time.
- Enables visual benchmarking of current performance versus past periods.

---

### 📊 Selected Measure by Day of Week (Center Right)
- **Custom-styled horizontal bar chart** showing `Selected Measure` aggregated by **Day of the Week** (Monday to Sunday)
- Helps uncover weekly performance patterns and peak activity days
- Dynamically updates based on the selected KPI (`Total Orders`, `Total Profit`, or `Total Sales`)

🔧 **Customization Details**:
- This is **not a standard bar chart**: day labels were removed from the Y-axis and manually positioned above each bar using **placeholder columns**
- This technique improves visual clarity and symmetry
- Inspired by this tutorial:  
  [YouTube – Custom Axis Labels in Power BI](https://www.youtube.com/watch?v=EiIAkJ9R7mM&t=518s)


---

### 📈 12-Month Rolling Total (Top Right)
- **Area chart** showing **12-month rolling sum** of the selected measure.
- Smooths out monthly fluctuations and highlights long-term performance trends.
- Useful for monitoring growth or decline with reduced seasonality noise.

---

### 📉 Monthly Value & 3-Month Moving Average (Bottom Right)
- **Line & area combo chart**:
  - Red line: actual monthly value of the selected measure
  - Dashed line: **3-month moving average**
- Supports short-term trend analysis and smoothing volatility.

---

### 🧠 Purpose of the Page
This page focuses on **temporal analysis**:
- How performance evolves over time
- Seasonal or weekly trends
- Rolling metrics for stability insights
- Year-over-year comparisons to detect momentum shifts

It supports decisions on timing, promotional cycles, and operational planning.

## 📦 Page 3 - Product & Category Performance Page
![Page 3 - Product & Category Performance Page](imgs/PNGs/3%20-%20Products.png)
This page focuses on product-level and category-level performance insights, highlighting the most profitable items and sales dynamics over time.

---

### 🏆 Most Profitable Category & Sub-Category (Top Right Cards)
- Two dynamic KPI cards showing:
  - Most profitable **Category**
  - Most profitable **Sub-Category**
- Based on total **profit** across all data.

---

### 📈 Top N Products by Selected Measure (Top Left Table)
- **Dynamic table** showing the top N performing products by:
  - Total Orders
  - Total Profit
  - Total Sales
- Controlled via a **Top N input box** and **Selected Measure button**
- Table includes:
  - Product ID & Name
  - Total Orders, Profit, Sales
  - Dynamic Rank
- Highlights high-performing SKUs for strategic focus.

---

### 🟠 Bubble Chart: Sub-Category Performance (Top Center)
- **Scatter plot (bubble chart)** comparing:
  - **X-axis**: Total Sales
  - **Y-axis**: Total Profit
  - **Bubble size**: Total Orders
  - **Color**: Product Category
- Provides a multidimensional view of sub-category performance:
  - Profitability
  - Sales volume
  - Order frequency
- Includes annotation (e.g., “Negative Profit”) to quickly spot underperformers.

---

### 🪄 Selected Measure by Quarter and Category (Bottom)
- **Ribbon chart** showing quarterly `Selected Measure` (Orders / Profit / Sales) split by **Category**:
  - Furniture
  - Office Supplies
  - Technology
- Supports **dynamic measure switching** via button selection
- Unlike a standard area chart, the **ribbon chart** shows:
  - **Rankings of categories** in each quarter
  - **Changes in category dominance** over time
- Ideal for analyzing seasonal trends and performance shifts between product categories

### 🧠 Purpose of the Page
This page is designed to:
- Identify the **most valuable products and sub-categories**
- Compare categories by **profitability**, **volume**, and **order count**
- Analyze **trends over time** and shifting performance by category
- Support decision-making for **inventory**, **product development**, and **marketing focus**

---

## 👥 Page 4 - Customer Insights Page
![Page 4 - Customer Insights Page](imgs/PNGs/4%20-%20Customers.png)
This page provides a deep dive into customer behavior, segmentation, and geographic distribution.

---

### ✅ KPI Cards (Top)
Three high-level performance indicators:
- **Total Customers**
- **Profit per Customer**
- **Sales per Customer**

These cards help evaluate customer base size and average value per customer.

---

### 🗺️ Total Customers by State (Left Map)
- **Map visual** using bubble size to represent number of customers in each U.S. state
- Helps identify regions with the largest customer concentration

---

### 📈 Total Customers by Month (Top Right)
- **Line and area chart** showing monthly customer count over time
- Includes a **trend line** to visualize long-term growth
- Useful for detecting customer acquisition patterns and seasonal variations

---

### 📊 %GT Total Profit by Customer Profit Segment (Bottom Left)
- **Bar chart** dividing customers into:
  - **Top 30% by Profit**
  - **Remaining 70%**
- Shows contribution to total profit:
  - Reveals heavy concentration of profit among top-performing customers

---

### 📊 %GT Total Sales by Customer Sales Segment (Bottom Center)
- **Bar chart** comparing:
  - Top 30% customers by sales
  - Remaining customers
- Highlights sales contribution imbalance within the customer base

---

### 🍩 Total Customers by Segment (Bottom Right)
- **Donut chart** showing distribution of customers across segments:
  - Consumer
  - Corporate
  - Home Office
- Supports marketing and strategy decisions based on customer types

---

### 🧠 Purpose of the Page
This page is designed to:
- Highlight geographic and temporal patterns in customer acquisition
- Reveal **80/20 dynamics** in profit and sales distribution
- Support **segmentation analysis** for marketing and retention strategies

## 📊 Page 5 - RFM Segmentation Page
![Page 5 - RFM Segmentation Page](imgs/PNGs/5%20-%20Customers%20RFM.png)
This page presents customer segmentation using the **Recency, Frequency, Monetary (RFM)** model to evaluate customer value and engagement levels.

---

### ✅ RFM Score Cards (Top)
Four KPI cards showing average scores:
- **Avg Recency Score**
- **Avg Frequency Score**
- **Avg Monetary Score**
- **Avg RFM Score** (overall average)

These metrics summarize customer engagement and value at a glance.

---

### 📦 Total Customers by RFM Customer Segment (Top Left)
- **Bar chart** showing customer count per RFM segment:
  - Churned / Inactive
  - At Risk / Sleeping
  - Promising / Average
  - Loyal & Valuable
  - Top Customer
- Helps identify the distribution of customer quality across the base.
- 🧰 **Custom Tooltip**: When hovering over each bar, a custom tooltip displays:
  - **Recency Score Distribution**
  - **Frequency Score Distribution**
  - **Monetary Score Distribution**
  - Each distribution is visualized as a histogram with average score line.
  - This allows better understanding of the segment’s internal RFM score spread and variance.

---

### 💰💵 Total & Average Profit and Sales by RFM Segment (Top Center, Top Right, Bottom Center, Bottom Right)

- Four **horizontal bar charts** grouped by **RFM Customer Segment**:
  - **Top Customer**
  - **Loyal & Valuable**
  - **Promising / Average**
  - **At Risk / Sleeping**
  - **Churned / Inactive**

- Displayed metrics:
  - **Total Profit** per segment
  - **Average Profit per Customer**
  - **Total Sales** per segment
  - **Average Sales per Customer**

- These visuals were built using the **same method** as the **"Selected Measure by Day of Week"** chart, with a focus on clean design and custom formatting:
  - Not standard bar charts.
  - Y-axis labels were manually removed.
  - Category labels were repositioned **above bars** using visual placeholders for cleaner layout.
  - Built with the help of this tutorial:  
    🎥 [YouTube: How to Create Better Bar Charts in Power BI](https://www.youtube.com/watch?v=EiIAkJ9R7mM&t=518s)

- These charts provide a comprehensive view of:
  - Which customer segments generate the most **revenue** and **profit**
  - **Per-customer value** within each segment
  - Strategic guidance for **retention**, **growth**, and **reactivation** efforts


---

### 🔄 Total and Average Orders by RFM Segment (Bottom Left)
- **Combo chart** with:
  - Red bars: Total Orders
  - Blue labels: Orders per Customer
- Highlights both volume and engagement per segment

---

### 🧠 Purpose of the Page
This page helps:
- Evaluate **customer value** through RFM segmentation
- Identify **loyal**, **high-spending**, and **at-risk** customers
- Support strategic decisions in **customer retention**, **personalized marketing**, and **resource allocation**
- Visualize both aggregate and per-customer metrics to guide targeting strategies


## 🗺️ Page 6 - Geographic Performance Page
![Page 6 - Geographic Performance Page](imgs/PNGs/6%20-%20Territory.png)
### 🎯 Purpose of the Page
This page highlights **territorial performance** by analyzing **Total Profit**, **Total Sales**, and **Top Locations** based on state and city. It helps identify key regions that drive business growth or underperform.

---

### 🏆 Most Profitable State & City (Top Right)
- Two KPI cards showing:
  - **State** with the highest total profit
  - **City** with the highest total profit
- Dynamically updates based on active slicers or filters.

---

### 📍 Top N Locations by Selected Measure (Top Left)
- A slicer allows choosing the **Top N** locations (states or cities) by selected measure.
- Segmented **toggle button** lets users switch between:
  - `Total Profit`
  - `Total Sales`
- Enables focused analysis of most profitable or highest revenue-generating locations.

---

### 📊 Top 5 Locations by Selected Measure (Bottom Left)
- **Bar chart** showing the **Top 5 States or Cities** by the selected measure.
- The visual is fully dynamic:
  - Changes based on selected KPI (profit/sales)
  - Automatically adjusts Top N count using the slicer
- Great for quick comparative analysis of regional performance.

---

### 🧭 Total Sales vs. Total Profit by State (Right)
- **Scatter plot** displaying:
  - **X-axis**: Total Sales
  - **Y-axis**: Total Profit
  - **Data points**: States (color-coded by profitability)
- Highlights:
  - High-sales but low-profit regions
  - States operating at **negative profit**
  - Strategic opportunities for optimization

- 📌 Tooltip includes State name and exact values.
- 🎯 Horizontal reference line for **zero-profit threshold**, visually separating profit vs. loss zones.
- 🔎 **Drill-through enabled**:
  - Right-clicking a state opens a drill-through page
  - Navigates to **city-level** performance for deeper geographic analysis


---

## 🧪 Product Drillthrough Page
![Product Drillthrough Pagee](imgs/PNGs/7%20-%20Product%20Detail.png)
### 🎯 Purpose of the Page
This drill-through page is designed to provide a **detailed performance breakdown** for any **selected product**. It is accessible from:
- **Top 25 Products by Selected Measure** on the **Overview Page**
- **Top N Products by Selected Measure** on the **Product & Category Performance Page**

Once a product is selected and drill-through is triggered, all visuals dynamically adjust to show data specific to that product.

---

### 🛒 Selected Product Banner (Top)
- Displays the **name of the selected product**.
- Visually confirms the drill-through context.

---

### 📈 Monthly Performance (Left)
- **Line chart** showing **Selected Measure** over time (month granularity).
- Includes a **trend line**.
- Enables performance trend tracking and seasonal pattern detection.

---

### 🗺️ Profit by State (Top Right)
- **Map visual** plotting **Selected Measure** by **U.S. state**.
- Bubble size corresponds to the value of the selected measure.
- Helps identify regional strengths and weaknesses.

---

### 🧮 Monthly Target KPIs (Bottom)
Three dynamic KPI gauges comparing actual values to target benchmarks:
1. **Monthly Orders vs. Target**
2. **Monthly Profit vs. Target**
3. **Monthly Sales vs. Target**

Each visual includes:
- Current month's actual value
- Projected target (based on last 3 non-zero months, +10%)
- Visual gauge indicating over/underperformance
- Values color-coded (e.g. red for negative performance)

---

### 🧠 Notes
- Targets are dynamically calculated using rolling logic.
- Values and visuals fully adjust based on the selected KPI.
- This page provides deep insight into **per-product** operational efficiency.

## 👤 Customer Segment Drillthrough Page
![Customer Segment Drillthrough Page](imgs/PNGs/8%20-%20Customers%20RFM%20Detail.png)
### 🎯 Purpose of the Page
This drill-through page provides **detailed insights into a specific RFM customer segment**. It is accessible directly from the **Customer RFM Page** by right-clicking on a segment name and selecting *Drill through*.

All visuals dynamically adjust based on the selected RFM segment, such as:
- **Top Customer**
- **Loyal & Valuable**
- **Promising / Average**
- **At Risk / Sleeping**
- **Churned / Inactive**

---

### 🔖 Selected Segment Banner (Top)
- Highlights the **currently selected RFM customer segment**.
- Visually confirms drill-through context.

---

### 📈 Total Orders by Month (Center Left)
- **Line chart** displaying **Selected Measure** over time.
- Trendline shows overall growth trajectory.
- Highlights seasonality and long-term engagement of customers in the selected segment.

---

### 🌡️ Customer Activity KPIs (Top Center)
Three key metrics summarizing segment behavior:
1. **Average Days Between Orders** – indicates frequency and engagement.
2. **Profit per Order**
3. **Sales per Order**

Each metric helps evaluate segment efficiency and profitability.

---

### 🗺️ Customers Heatmap by Location (Top Right)
- Heatmap based on customer location (by state).
- Darker shades represent higher concentrations of customers from the selected segment.
- Useful for identifying **geographic clusters of loyalty or churn**.

---

### 🧮 Total Orders by Category (Bottom)
- **Treemap chart** breaking down total orders by:
  - **Office Supplies**
  - **Furniture**
  - **Technology**
- Useful for identifying product preferences by customer segment.

---

### 🧠 Notes
- This page leverages dynamic filtering through the **Drillthrough** functionality in Power BI.
- All metrics are **fully responsive** to the selected segment.
- Supports better understanding of **segment-specific behavior**, useful for targeted campaigns, retention, or reactivation strategies.


## 📐 DAX Measures Documentation

All analytical measures were created in a dedicated table called **Measures Table**, grouped into thematic folders. These measures support KPI reporting, trend analysis, dynamic ranking, target tracking, and UX enhancements via slicers and dynamic titles.

All measures with description and DAX code can be found [here](measures/Measures.md).

---

### 📦 Orders

| Measure | Description |
|--------|-------------|
| **Total Orders** | Counts unique order IDs in the FactSales table. |
| **Monthly Orders Target** | Calculates a monthly order target as the average of the last 3 months with non-zero orders, increased by 10%. |
| **Orders Target Gap** | Calculates the difference between the target and actual number of orders. |
| **Orders per Customer** | Divides total orders by total distinct customers. |
| **Prev Month Total Orders** | Returns total orders from the previous month. |
| **Orders 3M Moving Average** | Calculates the 3-month moving average of total orders. |
| **Orders Rolling 12M** | Calculates total orders over the last 12 months. |
| **YTD Orders** | Calculates year-to-date order count. |
| **Total Orders Current Year** | Orders for the current calendar year. |
| **Total Orders Last Year** | Orders for the previous calendar year. |
| **%YoY Orders Change** | Percentage change in total orders compared to the previous year. |
| **Avg Days Between Orders** | Averages the number of days between purchases per customer (from DimCustomers). |

---

### 💰 Sales

| Measure | Description |
|--------|-------------|
| **Total Sales** | Sums the Sales column from FactSales. |
| **Monthly Sales Target** | Calculates a monthly target as average of the last 3 non-zero months of sales, increased by 10%. |
| **Sales Target Gap** | Difference between monthly sales target and actual sales. |
| **Sales per Customer** | Average sales value per customer. |
| **Sales per Order** | Average sales value per order. |
| **Prev Month Total Sales** | Sales in the previous month. |
| **Sales 3M Moving Average** | 3-month moving average of sales. |
| **Sales Rolling 12M** | Sales for the last 12 months. |
| **YTD Sales** | Year-to-date sales. |
| **Total Sales Current Year** | Sales for the current year. |
| **Total Sales Last Year** | Sales for the previous year. |
| **%YoY Sales Change** | Percentage YoY change in total sales. |
| **Top 30% of Customers Sales Threshold** | 70th percentile sales value across customers (top 30%). |
| **Total Sales by State** | Total sales without city-level filters (for state aggregation). |
| **Total Sales by City** | Total sales without state-level filters (for city aggregation). |
| **Top N Sales** | Calculates total sales for top N cities/states depending on user filters. |

---

### 📈 Profit

| Measure | Description |
|--------|-------------|
| **Total Profit** | Sums the Profit column from FactSales. |
| **Monthly Profit Target** | Similar to sales target – average of last 3 profitable months * 1.1. |
| **Profit Target Gap** | Difference between target profit and actual profit. |
| **Profit per Customer** | Average profit generated per customer. |
| **Profit per Order** | Average profit per order. |
| **Prev Month Total Profit** | Profit from previous month. |
| **Profit 3M Moving Average** | 3-month moving average of profit. |
| **Profit Rolling 12M** | Rolling sum of profit over 12 months. |
| **YTD Profit** | Year-to-date profit. |
| **Total Profit Current Year** | Profit for current calendar year. |
| **Total Profit Last Year** | Profit for previous calendar year. |
| **%YoY Profit Change** | Year-over-year profit growth. |
| **Top 30% of Customers Profit Threshold** | 70th percentile of customer profits. |
| **Total Profit by State** | Profit per state, regardless of city filters. |
| **Total Profit by City** | Profit per city, regardless of state filters. |
| **Top N Profit** | Calculates profit for top N locations based on filters. |

---

### 👥 Customers

| Measure | Description |
|--------|-------------|
| **Total Customers** | Distinct count of customer IDs. |

---

### 🧩 Slicers & Rankings

| Measure | Description |
|--------|-------------|
| **Products Rank by Selected Measure** | Ranks products dynamically based on the KPI selected (orders, sales, or profit). |
| **Products Top N by Selected Measure** | Shows ranking for Top N products based on selected KPI. Others get rank 0. |
| **Is Slicer Active** | Returns 1 if any slicer (year, region, category) is active, 0 otherwise. |
| **Active Slicers Message** | Generates a string message listing all active slicer values (Year, Region, Category). |

---

### 📊 Time Trends – Titles

| Measure | Description |
|--------|-------------|
| **Day Name Labels** | Returns selected weekday name from DimCalendar. |
| **Day Name Placeholder** | Returns 0, placeholder for visuals. |
| **Selected Measure by Day Name - Title** | Dynamic title for KPI by day of week charts. |
| **Selected Measure (Totals and MA) by Month - Title** | Title for KPI and 3M MA trend over months. |
| **Selected Measure (RT) by Month - Title** | Title for 12-month rolling total trends. |
| **Selected Measure (YTD) by Month - Title** | Title for year-to-date trends. |

---

### 🏷️ Dynamic Titles – General

| Measure | Description |
|--------|-------------|
| **Customer RFM Segment Labels** | Returns the RFM segment of selected customer. |
| **Customer RFM Segment Placeholder** | Returns 0 – used to stabilize visual layouts. |
| **Dummy Title** | Returns empty string – placeholder for cards. |
| **Top 25 Products by Selected Measure - Title** | Static title for top 25 products depending on selected KPI. |
| **Top N Products by Selected Measure - Title** | Fully dynamic title based on selected Top N value and KPI. |
| **Top N Locations by Selected Measure - Title** | Dynamic title for maps or tables based on selected KPI and Top N value. |

---

### 🧠 Notes

- All `%YoY Change` measures are calculated using current year vs. previous year values from the calendar table.
- Moving averages are calculated using `DATESINPERIOD` for clean time-intelligence performance.
- Top N logic is consistent across products, cities, and states – dynamic and slicer-controlled.
- Titles and placeholders enhance UX without affecting core metric logic.

## 📊 Most Complex DAX Measures

This section highlights the most advanced and dynamic DAX measures used in the project. These calculations combine variable definitions, conditional branching, context-sensitive filters, and dynamic logic to support flexible and user-driven analytics.

---

### `Top N Sales`
Dynamically shows Top N states or cities depending on which level of the `State → City` hierarchy is currently displayed on the X-axis of the bar chart.


```dax
VAR n = 'Top N Territory'[Top N Territory Value]

VAR topCities =
    TOPN(n, ALLSELECTED(DimTerritory[City]), [Total Sales by City])

VAR topCitiesInState =
    TOPN(
        n, 
        FILTER(
            ALLSELECTED(DimTerritory[State], DimTerritory[City]),
            DimTerritory[State] = MAX(DimTerritory[State])
        ), 
        [Total Sales by City]
    )

VAR topStates =
    TOPN(n, ALLSELECTED(DimTerritory[State]), [Total Sales by State])

RETURN
    SWITCH(
        TRUE(),
        ISINSCOPE(DimTerritory[City]) && NOT(ISINSCOPE(DimTerritory[State])),
            CALCULATE([Total Sales by City], KEEPFILTERS(topCities)),

        ISINSCOPE(DimTerritory[City]) && ISINSCOPE(DimTerritory[State]) && DISTINCTCOUNT(DimTerritory[State]) = 1,
            CALCULATE([Total Sales by City], KEEPFILTERS(topCitiesInState)),

        ISINSCOPE(DimTerritory[State]) && NOT(ISINSCOPE(DimTerritory[City])),
            CALCULATE([Total Sales by State], KEEPFILTERS(topStates)),

        BLANK()
    )
```
**What it does**:  
Returns the top N sales for geographic locations, dynamically adjusting to whether the visual shows states or cities. It uses slicer-driven logic and dynamic filtering with `ISINSCOPE`, `TOPN`, and `KEEPFILTERS`.

> This measure was particularly challenging to implement. It required significant time and iteration, eventually leading to a post on the official Power BI Community forum for guidance:  
> [Filter top-N elements on both levels of hierarchy](https://community.fabric.microsoft.com/t5/Desktop/Filter-top-N-elements-on-both-levels-of-hierarchy/m-p/4789542#M1426101)


### `Products Rank by Selected Measure`

Ranks products based on the user-selected KPI: Total Sales, Profit or Orders
```dax
SWITCH(
    TRUE,
    SELECTEDVALUE('KPI Measures'[KPI Measures Fields]) = "'Measures Table'[Total Orders]",
    RANKX(ALLSELECTED(DimProducts), [Total Orders], , DESC),

    SELECTEDVALUE('KPI Measures'[KPI Measures Fields]) = "'Measures Table'[Total Profit]",
    RANKX(ALLSELECTED(DimProducts), [Total Profit], , DESC),

    SELECTEDVALUE('KPI Measures'[KPI Measures Fields]) = "'Measures Table'[Total Sales]",
    RANKX(ALLSELECTED(DimProducts), [Total Sales], , DESC)
)
```
**What it does**:  
Ranks each product according to the KPI selected by the user. This allows a single visual to switch between rankings by Orders, Sales, or Profit using a disconnected slicer table.

### `Monthly Profit Target`
Calculates a dynamic monthly profit target based on a 3-month average with a 10% uplift
```dax
VAR currentMonth = MAX(DimCalendar[Start of month])

VAR validMonths =
    TOPN(
        3,
        FILTER(
            ALL(DimCalendar[Start of month]),
            DimCalendar[Start of month] < currentMonth &&
            [Total Profit] > 0
        ),
        DimCalendar[Start of month],
        DESC
    )

RETURN 
    ROUNDUP(
        AVERAGEX(validMonths, [Total Profit]) * 1.1, 0
    )
```
**What it does**:  
Calculates a forward-looking monthly target based on the average of the last 3 months of non-zero orders, with a 10% growth margin. Useful for target vs. actual KPIs and trend tracking.  
Analogous measures have been created for Monthly Sales and Monthly Profit targets using the same logic.


## 🎨 UX/UI Design

### 🎨 Layout & Color Scheme

The report uses a **clean, card-based layout** applied consistently across all pages to enhance user orientation and reduce cognitive load.  
Fixed placement of KPI cards, slicers, and visuals ensures a predictable and efficient user experience.

A **vibrant and cohesive color palette** is applied throughout the report.  
> 🎨 **Palette Source**: [AI Colors by BairesDev](https://www.bairesdev.com/tools/ai-colors)  
> 🎨 **Selected Theme**: `#DE283B`

High contrast and generous whitespace improve accessibility and readability across all devices.

---

### 🧭 Navigation Sidebar

All main report pages include a **vertical navigation bar** on the left with **icon buttons** for seamless navigation:

- 🧪 Filter Panel (top icon)
- ℹ️ Info / Slicer Indicator
- 🏠 Homepage
- 📈 Time Trends
- 📦 Product Overview
- 👥 Customer Segments
- 🔁 RFM Segments
- 🌍 Territory Overview

Each icon is styled in **white** and linked to corresponding report pages via **bookmarks**.

---

### 📂 Collapsible Filter Panel

The navigation bar includes a **Filter button** (funnel icon) that toggles a collapsible filter panel with the following slicers:

- **Year**: 2014, 2015, 2016, 2017  
- **Region**: Central, East, South, West  
- **Category**: Furniture, Office Supplies, Technology  

Slicers are styled in **rounded containers** with layout matching the sidebar's gradient for visual cohesion.  
This panel stays hidden by default to **maximize report space**, but can be summoned when needed.

---

### ⚠️ Dynamic Filter Status Indicator

The **Info icon** (`ℹ️`) serves as a **visual indicator** of applied filters:

- Default: **white icon**
- Filters active: **yellow icon**

On hover, a **tooltip** shows currently applied slicers, e.g.:

> `Applied Slicers – Year: 2014  Region: Central  Category: Furniture`

This provides **transparency** even when the slicer panel is collapsed.

---

### 🔘 Global Feature – Dynamic KPI Toggle (Orders / Profit / Sales)

A custom **button toggle** is implemented across multiple report pages to switch dynamically between the three core KPIs:
- `Total Orders`
- `Total Profit`
- `Total Sales`

#### 🔧 Technical Implementation:
- The button is linked to a **bookmark** that updates a hidden slicer.
- This slicer controls which measure is used via DAX logic (`SWITCH` + `SELECTEDVALUE`).
- **Why a button instead of a visible slicer?**  
  The button allows better visual customization and cleaner UI than a default slicer.

This approach lets a single page support **complex KPI analysis** without duplicating visuals, ensuring scalability and consistency.

---
### 🎯 Focus on Key Insights

- **Top-aligned KPI cards** highlight key metrics at a glance.
- Each page is focused on one **analytical goal or business question**.
- Visuals are grouped logically to accelerate insight discovery and user understanding.

---

### 🤝 Interactivity & Navigation

- Dynamic **KPI selectors** (Orders / Profit / Sales) simplify layout and reduce visual noise.
- **Drill-through navigation** enables detailed analysis:
  - From product lists → product performance page
  - From RFM charts → segment-level insights
  - From territory maps → city-level breakdown
- **Top N sliders** allow quick exploration of best-performing entities.

---

### 🧠 Custom Visual Design

- The **day-of-week chart** uses a custom trick:  
  - Y-axis is hidden, and weekday labels are manually placed above bars using placeholders.  
  - Based on [this tutorial](https://www.youtube.com/watch?v=EiIAkJ9R7mM&t=518s)

- Visuals such as:
  - RFM histograms
  - Total vs. Avg metrics by segment
  - Scatter plots for profit vs. sales  
  include **custom tooltips** to enrich interpretation and storytelling.

---

### 🌐 Accessibility & Readability

- Large, legible fonts with strong contrast support users with mild vision impairments.
- Whitespace and layout spacing are used to **group content visually**, enhancing scannability.
- Color cues, tooltips, and icons assist with orientation and filtering feedback.

---

### ⚙️ Performance & Optimization

- DAX **measures** are used instead of calculated columns to optimize model performance.
- Pages include a **minimal number of visuals and slicers**, balancing insight with speed.
- Titles, tooltips, and visual elements dynamically update using **DAX logic** and bookmarks, enabling flexible, responsive design.

## 📌 Key Insights

The dashboard provides clear and actionable insights across multiple business dimensions.  
Below are the **main discoveries** enabled by the report:

---

### 🧪 Product & Sales Insights
- A small number of **top-performing products** generate a **disproportionate share of profit and sales**.
- Some products with **high sales** still deliver **negative or low profit**, indicating potential pricing or cost issues.
- **Technology** consistently outperforms other categories in both sales and profitability.

---

### 👥 Customer Behavior
- The majority of profit comes from **Top Customers** and **Loyal & Valuable** segments.
- **Churned/Inactive** and **At Risk** customers make up a large portion of the base but generate minimal revenue.
- There's a strong correlation between **average order value** and **RFM score**, especially within the **Top Customer** segment.

---

### 📈 Time & Seasonality
- **Monthly sales and profit** show clear **seasonal trends**, with peaks at the end of each year.
- Weekly activity shows spikes around **Tuesdays and Fridays**, depending on the metric.
- Certain months fall **below projected targets**, helping to identify underperforming periods.

---

### 🌍 Geography
- **California** and **New York** are the most **profitable territories** by a large margin.
- Several states (e.g. **Texas**, **Florida**) operate at a **net loss**, suggesting the need for strategy reevaluation.
- Drill-through analysis by state/city enables deeper understanding of local market dynamics.

---

### 📊 RFM Distribution
- Most customers have **moderate recency and frequency scores**, but **high monetary scores** are rare.
- **Loyal & Valuable** customers are the most active and generate the highest revenue per order.
- Segment-based analysis reveals opportunities for **targeted marketing** and **retention strategies**.

---

These insights support both **high-level strategic decisions** and **tactical day-to-day actions** across sales, marketing, and customer success teams.


## ⚠️ Challenges & Learnings

Throughout the development of this report, several technical and design challenges emerged.  
Overcoming them led to meaningful skill development and creative problem-solving:

### 🧠 Key Challenges

- **Top N by Hierarchy Level (State → City)**  
  Creating a dynamic Top N chart that adapts based on whether **state** or **city** is in scope required advanced use of `ISINSCOPE`, `TOPN`, and `KEEPFILTERS`.  
  Solution involved a complex measure with conditional logic.  
  Final version shared and discussed on [Power BI Community Forum](https://community.fabric.microsoft.com/t5/Desktop/Filter-top-N-elements-on-both-levels-of-hierarchy/m-p/4789542#M1426101).

- **Forward-Looking KPI Targets**  
  Developing DAX measures that calculate a monthly target based on the average of the **last 3 non-zero months**, then apply a **+10% growth margin**.  
  Required careful filtering and use of variables to avoid zero months.

- **Custom Tooltip for RFM Segments**  
  Displaying Recency, Frequency, and Monetary distribution inside a tooltip panel required designing **hidden pages** and **slicer syncs**, improving storytelling without cluttering the main view.

- **Slicer Panel with Filter Indicator**  
  Designing a collapsible slicer panel combined with a **dynamic info icon** that changes color when filters are active.  
  Improved UX and reduced layout noise while maintaining filter transparency.

---

### 📚 What I Learned

- Advanced **DAX techniques**: `ISINSCOPE`, `TOPN`, `KEEPFILTERS`, variables, dynamic switching.
- Effective **UX design in Power BI**, including bookmarks, hidden slicer panels, conditional icons.
- Optimizing for **performance** by avoiding calculated columns and using optimized relationships.
- Using community resources and forums as a problem-solving aid.
