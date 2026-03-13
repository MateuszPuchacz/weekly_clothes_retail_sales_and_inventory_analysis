# weekly_clothes_retail_sales_and_inventory_analysis

## 🎯 Project Goal

This project simulates the analytical workflow I currently perform in my professional role in retail clothes sales and inventory analysis.
The repository presents a simplified version of Excel based reporting structures used to analyze weekly sales performance and product inventory. The dataset included in this project was generated with AI support and manually adjusted to resemble real business data while remaining fully simulated for portfolio purposes.


## 📥 Data Collection

At the beginning of each week, sales data from the previous week as well as cumulative sales data are exported from Tableau.
However, the Tableau reports don't contain all product attributes required for detailed analysis,for clothes.
Additionally, the reporting system doesn't allow exporting both weekly and cumulative sales data for articles in a single report. Because of this limitation, I need to extract two separate datasets and then integrate them into a single analytical structure.
To combine these datasets efficiently, I use Excel-based matrices built on pivot table logic, which allow me to align and merge the results from both exports. This approach significantly speeds up the data preparation process and enables consistent comparison between weekly and cumulative performance.


## 🧩 Data Enrichment

To complete the dataset, additional product information is retrieved using Excel lookup functions (primarily VLOOKUP) from supplementary files stored locally.

These files contain key product attributes such as:

- Model number

- Color

- Size

- Initial selling price

- Transfer price

- Season classification (Winter / Summer)

- Regional coordinator responsible for a product group


Each product has a unique product number, which allows missing attributes to be matched and appended to the Tableau export files.
During this stage, basic **data cleaning 🧹 and validation 🧱** is also performed to ensure data consistency. This includes checking for missing values, verifying product identifiers, standardizing attribute formats, and removing inconsistencies between the exported datasets and the reference product lists.

## ⚙️ Product Data Management

As part of my responsibilities, I also maintain internal product reference files used for data enrichment. This includes:

- assigning product codes in internal company systems

- uploading product prices to stores system

- maintaining seasonal product lists

- organizing articles by year and season

- creating consolidated product reference tables

These structured files serve as lookup tables that allow missing attributes to be automatically appended to the main dataset.

In my current role I'm responsible for three product departments, and I process approximately 1 million records per week.
Due to corporate system limitations (access restricted to Excel), the data is distributed across multiple files to stay within Excel row limits.


## ⚠️ Data Disclaimer

All datasets used in this repository are fully simulated and were generated with AI assistance and manual adjustments. The structure of the files reflects real analytical workflows what I do, but the data itself does not contain any confidential or proprietary business information.
Despite being simulated, the dataset preserves realistic business logic and allows the creation of meaningful analytical insights. The results presented in this project demonstrate how data can be explored, interpreted, and transformed into business storytelling similar to real retail analysis.



## 🛠 Tools & Technologies

- **Microsoft Excel** – used to prepare the business results file, integrate datasets, and structure the analytical model.
- **AI (ChatGPT)** – used to generate the simulated dataset included in the **"data"** worksheet.


## ⚙️ Excel Report Automation Logic


While the first report provides a high level overview of inventory and sales performance,
the second report allows deeper analysis at category, subcategory and store level.

## Excel Reporting Architecture

The Excel reporting model follows a layered structure where pivot tables act as the aggregation layer and automated reports transform the data into business insights.
```
Raw Data
   ↓
Pivot Tables (tp_cat, tp_cat2, T1, T2)
   ↓
Data Mapping (VLOOKUP / Direct Cell References)
   ↓
Calculated KPI Metrics
   ↓
Automated Reports & Dashboards
```
This structure allows the Excel file to function as a lightweight reporting system combining data aggregation, automated calculations and analytical reporting.

Additionally, the file contains several sheets with simple pivot tables used for quick situational analysis depending on the current needs of the analyst and stakeholders.


## **REPORT 1️⃣**

**Dashboard Logic:**

The first report acts as the main automated dashboard, presenting a high level overview of stock and sales performance across product categories.
The dashboard retrieves aggregated results from pivot tables and transforms them into structured business metrics using lookup formulas and calculated indicators.

![Report1](./images/Report1.png)
**The full report screenshot is included here to present the overall structure and logic of the file. Due to its size, specific sections of the report will be shown separately below in " Exploratory Business Analysis" to provide clearer analysis and better readability.**

**Data Retrieval**

Data is dynamically retrieved from pivot tables using VLOOKUP formulas with dynamic column references.
This allows the dashboard to automatically update whenever the pivot tables are refreshed while maintaining a consistent report structure.


Two pivot tables act as the data aggregation layer:

tp_cat 

Provides total results by category and feeds the upper section of the dashboard:
Week & Total currently season


This section summarizes overall stock and sales performance.

tp_cat2 

This pivot table provides a more detailed breakdown of the data, including:
product typology (STD, EXC, COUNTRY, OLD)

The results are structured using category connectors  in columne "A" which allow the dashboard to dynamically retrieve values from the pivot table.


**Dynamic Data Retrieval**

The dashboard retrieves values from pivot tables using a dynamic lookup formula:

```
=IFERROR(VLOOKUP($B7;tp_cat!$A:$AE;C$1;0);" ")

Key elements of this approach:

$B7 – category used as lookup key
tp_cat / tp_cat2 – pivot table data sources
C$1 – dynamic column index controlled by header values
IFERROR – prevents lookup errors when data is missing
```
Numbers placed in the header rows act as column index references, allowing the same formula to populate the entire dashboard without manually adjusting column numbers.

This high-level report serves as the starting point for analysis, while the second report enables deeper exploration at category and store level.



## **REPORT 2️⃣**

Detailed Category & Subcategory Report per total & stores
The second report provides a more granular view of inventory and sales performance, allowing analysis by category, subcategory and individual stores.
The report is powered by two pivot tables, which act as the data aggregation layer.

![Report2_1](./images/Report2_1.png)
![Report2_2](./images/Report2_2.png)
![Report2_3](./images/Report2_3.png)

**The screenshots above are provided only to illustrate the functionality and structure of Report 2. The main business analysis in this project will be based primarily on Report 1 and few pivot tables, which presents the overall situation of the stock and sales. Report 2 serves mainly as a supporting analytical tool that allows deeper exploration of categories, subcategories and store-level results. The images are included here only to visualize how the report is structured.**



Pivot Table Data Sources

Two pivot tables supply the report:

**T1**

This pivot table provides aggregated results including:

- product categories
- subcategories
- product typologies (STD, EXC, COUNTRY, OLD)

The data from this pivot table feeds the Total view of the report, allowing users to analyze overall performance.

**T2**

This pivot table contains the same structure as **T1** but includes an additional breakdown per store, allowing detailed performance analysis for each location.

**Direct Cell References**

Unlike the first dashboard which uses VLOOKUP, this report retrieves data using direct cell references from the pivot tables.
This approach allows the report to update automatically whenever the pivot tables are refreshed.
The total section always contains a fixed number of rows, ensuring consistent structure for the aggregated view.
When analyzing individual stores, the number of rows may vary depending on the available data. In cases where fewer rows exist, empty results appear as 0 values, while additional records can be quickly incorporated by extending formulas downward.


**Subtotals**

Subtotals were added above the column headers using Excel SUBTOTAL functions, allowing the report to dynamically recalculate totals when filters are applied.
This enables flexible analysis depending on selected views.

**Report Navigation**

The report can be analyzed at two different levels.

**Total View**

By selecting TOTAL in the Store or Store Number filter, users can analyze the overall performance across all stores.
Subcategory value 0 is excluded from the view, as it represents aggregated totals rather than individual product groups.

**Store-Level View**
To analyze a specific store, users simply select the desired store name from the filter.
For example:
Selecting Białystok displays the full category and subcategory performance for that store.

**Reporting Logic**

The report follows the structure below:
This structure enables flexible analysis across both overall performance and store-level results.


## 📈 **Key Retail Metrics Explained**


The dashboard focuses on several key metrics commonly used in retail inventory and sales analysis.
These indicators help evaluate stock efficiency, pricing strategy and sales performance.

Average Purchase Price measures the average cost at which products were purchased.
This metric helps monitor whether procurement costs change over time and supports margin analysis.
```
=Total Purchase Value / Stock Quantity
2024: =IFERROR(G7/C7;"")
2025: =IFERROR(H7/D7;"")
```


Average Selling Price

Average Selling Price measures the average price at which products were sold.
This KPI helps identify pricing trends and evaluate the effectiveness of pricing strategies.

```
=Total Sales Value / Units Sold
2024: =IFERROR(O7/K7;"")
2025: =IFERROR(P7/L7;"")
```

% Resale

The Resale Percentage shows what portion of the available stock was sold during the analyzed period.

```
=Sales Quantity / (Sales Quantity + Stock Quantity)
2024: =IFERROR(K7/(K7+C7);"")
2025: =IFERROR(L7/(L7+D7);"")
```

Weeks of Stock (WOS) / Stock Coverage (SC)

Weeks of Stock shows how many weeks the current inventory can support sales at the current sales pace.

```
=Stock Quantity / Weekly Sales
2024: =IFERROR(C7/K7;"")
2025: =IFERROR(D7/L7;"")
```

Year-over-Year Value Difference

Year-over-Year value difference shows the absolute change between two periods.

```
=Current Year Value - Previous Year Value
=IFERROR(D7-C7;"")
```

Year-over-Year Change (%)

Year-over-Year percentage change measures the relative growth or decline between two periods.

```
=(Current Year Value / Previous Year Value) - 1
=IFERROR(D7/C7-1;"")
```

 
## 🎨 Conditional Formatting

Conditional formatting was applied to the Year-over-Year indicators:

- Prog %

- Prog Value

Negative values are automatically highlighted in red, which allows users to quickly identify declines in performance compared to the previous year.

This visual rule helps highlight situations where:

- stock decreased

- sales dropped

- resale performance weakened

By automatically emphasizing negative changes, the report makes it easier to detect potential issues in inventory or sales dynamics without manually reviewing each value.

```
Conditional rule: Value < 0 → red text
```




## 📊 Exploratory Business Analysis


**Currently Season (STD +EXC)**

**Last Week:**

![week_cs_1](./images/week_cs_1.png)
**Key observations**

- Total inventory decreased significantly from 273 658 units to 208 126 units (-24% YoY), while weekly sales increased from 372 440 to 444 922 units (+19% YoY).

- This indicates a strong improvement in inventory productivity, where a smaller stock base is generating higher weekly sales.

**The strongest weekly growth was observed in:**

- T-shirts and shirts: +22% weekly sales

- Sweatshirts and sweaters: +25% weekly sales

- Outerwear: +35% weekly sales

Despite lower stock levels in several categories, demand remained strong, suggesting better assortment selection before the season.

However, margin dynamics show some pressure:

- Weekly margin value increased +10%, but

- Margin % decreased from 32% to 30% (-2 pp).

This suggests that sales growth was partly supported by pricing actions or promotional activity.

**Commercial insight**

The current season assortment is generating higher weekly sales with significantly lower inventory levels, indicating improved demand alignment and stronger product productivity.


![week_cs_2](./images/week_cs_2.png)
**Key observations**

- Average selling price declined from 23.59 to 22.00 (-7%), indicating stronger promotional pressure or pricing adjustments.
- Average purchase price decreased slightly (-2%), meaning that the majority of margin pressure comes from retail price reductions rather than purchasing cost changes.
- Resale increased from 5% to 9% (+4 pp), indicating significantly faster stock rotation.
- Weeks of stock decreased from 17 weeks to 10 weeks (-7 weeks), which confirms a much leaner inventory structure.

**Category observations:**

- Pants and shorts show improved resale (7% → 11%) with reduced weeks of stock (13 → 8 weeks), indicating strong demand.
- T-shirts and shirts improved resale (7% → 10%) while reducing stock coverage (14 → 9 weeks).
- Outerwear reduced stock coverage significantly (65 → 33 weeks), suggesting aggressive stock reduction in this category.

**Commercial insight**

Improved resale combined with lower weeks of stock confirms that the assortment is turning faster and carrying significantly less over inventory risk.

**TOTAL:**

![total_cs_1](./images/total_cs_1.png)

**Key observations**

- Total sales volume decreased only slightly from 57,747 units to 56,041 units (-3%), despite a 24% reduction in total inventory levels compared to the previous year.
- Gross sales value declined more noticeably (-11% YoY), mainly due to lower average selling prices across several categories.
- Margin value decreased by 16%, while margin percentage declined moderately from 32% to 30% (-2 pp).
- The pricing data confirms a reduction in average selling price (-7%), indicating stronger promotional activity and price adjustments implemented to support sell-through and inventory reduction.

Commercial insight

The results reflect a deliberate inventory reduction strategy implemented in 2025.

The company intentionally reduced stock levels across stores in order to eliminate excess inventory accumulated in the previous season.
Despite the significant stock reduction, sales volume remained relatively stable (-3%), which suggests that the previous inventory levels were higher than necessary to support demand.
The data indicates that the assortment was better aligned with actual customer demand, allowing the company to operate with a leaner inventory structure without materially impacting sales performance.
At the same time, lower retail prices helped accelerate stock rotation and support the inventory clean-up process, even though this resulted in some pressure on margin value.

**STD vs EXC separated**

**Last Week:**

![std_exc_1](./images/std_exc_1.png)
Key observations

The weekly results clearly show different performance dynamics between STD (standard assortment) and EXC (promotional assortment).

The STD segment experienced a reduction in weekly sales:

- 8,934 → 8,412 units (-6%)
- Weekly gross sales decreased -5%
- Weekly margin value declined -9%

This reflects a deliberate reduction of stock levels in the core assortment, which resulted in slightly lower weekly sales.

In contrast, the EXC segment recorded strong growth:

- Weekly sales increased 6,856 → 11,924 units (+74%)
- Weekly gross sales increased +53%
- Weekly margin value increased +36%

This suggests that promotional products played a key role in driving demand during the analyzed week.

💡 Commercial insight
The weekly performance indicates a clear shift in sales dynamics where EXC products compensated for weaker STD sales, supporting overall demand despite reduced inventory in the core assortment.


![std_exc_2](./images/std_exc_2.png)
Key observations

The pricing and inventory indicators highlight clear structural differences between STD and EXC assortments.

For the STD segment:

-  Average selling price remained relatively stable (+1.3%)
- Resale increased from 4% to 6%
- Weeks of stock decreased from 23 to 17 weeks

This confirms that inventory reduction improved stock turnover efficiency in the standard assortment.

For the EXC segment:

- Average selling price decreased significantly (-11.9%)TETA
- Average selling price decreased significantly (-11.9%)TETA
- Resale increased strongly (10% → 15%)

Weeks of stock decreased from 9 to 6 weeks

This suggests that promotional pricing accelerated product rotation, allowing the business to reduce inventory exposure faster and oranizing new deliveries.

Commercial insight

EXC products show significantly faster inventory turnover, confirming that promotional assortment plays a key role in clearing inventory and supporting sell through.

**TOTAL**
![std_exc_3](./images/std_exc_3.png)


Key observations

The total season results reveal a structural shift in sales contribution between STD and EXC assortments.

The STD segment recorded a decline across most indicators:

- Sales volume decreased 38,818 → 28,216 units (-27%)
- Sales value decreased -28%
- Margin value declined -30%

This reflects the intentional reduction of stock levels within the core assortment.

In contrast, the EXC segment delivered strong growth:

Sales volume increased 18,929 → 27,825 units (+47%)
Sales value increased +25%
Margin value increased +12%

This indicates that promotional products became a much stronger driver of total sales performance in the current season.

Commercial insight:

The results suggest that the company strategically reduced exposure to standard inventory while leveraging promotional assortment to maintain sales momentum and improve inventory turnover.


