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

**💡 Commercial insight**

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

**💡 Commercial insight**

Improved resale combined with lower weeks of stock confirms that the assortment is turning faster and carrying significantly less over inventory risk.

**TOTAL:**

![total_cs_1](./images/total_cs_1.png)

**Key observations**

- Total sales volume decreased only slightly from 57,747 units to 56,041 units (-3%), despite a 24% reduction in total inventory levels compared to the previous year.
- Gross sales value declined more noticeably (-11% YoY), mainly due to lower average selling prices across several categories.
- Margin value decreased by 16%, while margin percentage declined moderately from 32% to 30% (-2 pp).
- The pricing data confirms a reduction in average selling price (-7%), indicating stronger promotional activity and price adjustments implemented to support sell-through and inventory reduction.

**💡 Commercial insight**

The results reflect a deliberate inventory reduction strategy implemented in 2025.

The company intentionally reduced stock levels across stores in order to eliminate excess inventory accumulated in the previous season.
Despite the significant stock reduction, sales volume remained relatively stable (-3%), which suggests that the previous inventory levels were higher than necessary to support demand.
The data indicates that the assortment was better aligned with actual customer demand, allowing the company to operate with a leaner inventory structure without materially impacting sales performance.
At the same time, lower retail prices helped accelerate stock rotation and support the inventory clean-up process, even though this resulted in some pressure on margin value.

**STD vs EXC separated**

**Last Week:**

![std_exc_1](./images/std_exc_1.png)

**Key observations**

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

**💡 Commercial insight**

The weekly performance indicates a clear shift in sales dynamics where EXC products compensated for weaker STD sales, supporting overall demand despite reduced inventory in the core assortment.


![std_exc_2](./images/std_exc_2.png)

**Key observations**

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

**💡 Commercial insight**

EXC products show significantly faster inventory turnover, confirming that promotional assortment plays a key role in clearing inventory and supporting sell through.

**TOTAL**
![std_exc_3](./images/std_exc_3.png)

**Key observations**

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

**💡 Commercial insight**

The results suggest that the company strategically reduced exposure to standard inventory while leveraging promotional assortment to maintain sales momentum and improve inventory turnover.



**Country & OLD**




![country_old_1](./images/country_old_1.png)
Key observations

The Country assortment shows strong weekly sales dynamics despite a significant reduction in inventory levels.

Total stock decreased from 283,669 units to 187,632 units (-34%), while weekly sales increased significantly:

- 20,668 → 35,174 units (+70%)
- Weekly gross sales increased +47%
- Weekly margin value increased +14%

The strongest growth can be observed in:

- T-shirts and shirts: +78% weekly sales
- Pants and shorts: +126% weekly sales
- Underwear: +62% weekly sales

This indicates that locally sourced products generated strong demand during the analyzed week.

**💡 Commercial insight**

Country products appear to play an important role as a flexible supporting assortment, allowing the company to react quickly to demand and complement the main collection.


The OLD assortment shows the expected dynamics typical for previous season products.

Inventory levels were significantly reduced:

- 99,683 → 59,696 units (-40%)

Weekly sales decreased slightly:

- 5,252 → 4,785 units (-9%)

However, margin value increased +28%, indicating that remaining products still generate value despite lower sales volumes.

**💡 Commercial insight**

The OLD assortment is being gradually cleared while still generating margin, which suggests effective inventory reduction without excessive discounting.



![country_old_2](./images/country_old_2.png)

Country – Pricing and Inventory Efficiency


Key observations

Inventory efficiency indicators show a significant improvement in stock turnover.

- Resale increased from 7% to 16%
- Weeks of stock decreased from 14 to 5 weeks

This indicates much faster inventory rotation compared to the previous season.

At the same time:

- Average selling price decreased -13.6%
- Average purchase price decreased -9.8%

This suggests that pricing adjustments helped stimulate demand while maintaining acceptable margin levels.

**💡 Commercial insight**

Country assortment shows very efficient stock rotation, confirming that locally sourced products can be used to quickly generate sales and improve inventory turnover.

💰 OLD – Pricing and Inventory Efficiency


Key observations

Pricing indicators show moderate adjustments in order to support sell-through of older collections.

- Average selling price increased +16.6%
- Average purchase price increased +8.6%

Resale improved slightly:

- 5% → 7%

Weeks of stock decreased from 19 to 12 weeks, indicating gradual reduction of remaining inventory.

**💡 Commercial insight**

The improvement in resale and reduction in weeks of stock suggests that the company is successfully managing the clearance process of older collections.


![country_old_3](./images/country_old_3.png)

📈 Country – Total Season Performance


Key observations

The total season results confirm strong growth in the Country assortment:

- Sales volume increased 40,555 → 68,892 units (+70%)
- Gross sales increased +38%
- Margin value increased +2%

Despite strong sales growth, margin percentage decreased from 28% to 21% (-7 pp).

This decline indicates stronger price competition and promotional pricing in order to support demand growth.

**💡 Commercial insight**

The Country assortment significantly increased its contribution to total sales, suggesting that locally sourced products became an important demand driver during the season.

📈 OLD – Total Season Performance


Key observations

Total seasonal performance confirms the ongoing inventory reduction strategy for previous collections.

- Sales volume decreased 23,447 → 17,283 units (-26%)
- Gross sales decreased -13%

However:

- Margin value increased +8%
- Margin percentage improved 19% → 24% (+5 pp)

This suggests that despite lower sales volumes, the remaining assortment is being sold with improved profitability.

**💡 Commercial insight**

The OLD assortment is being successfully reduced while maintaining margin performance, indicating effective stock clearance management.


**📊 Final Business Insights**

The analysis shows a clear shift in assortment and inventory strategy during the 2025 season.

Total inventory levels were significantly reduced across the business:

- Current Season: −24%
- Country assortment: −34%
- Old collections: −40%

Despite this reduction, sales performance remained relatively stable. Total sales volume for the current season decreased only −3%, while weekly sales increased +19%, indicating a much better alignment between supply and demand.

Sales dynamics shifted across assortment types:

- STD assortment declined (−27% sales volume) mainly due to intentional inventory reduction.
- EXC assortment became a key growth driver with +47% sales volume supported by promotional and licensed products.
- Country assortment showed strong growth (+70% sales volume), proving effective as a flexible complement to the main collection.
- OLD assortment continued to decline (−26% sales volume) as part of the inventory clean-up strategy.

Pricing adjustments also played a role in supporting demand. Average selling prices declined across several categories, which helped improve inventory turnover and resale rates.

Overall, the data suggests that the company successfully moved toward a leaner and more demand-driven assortment structure, maintaining stable sales performance while significantly reducing inventory.

**📊 Additional Pivot Analysis**

In addition to the main analytical reports, several supplementary pivot tables were created to explore specific operational aspects of the business from different perspectives.
Pivot tables allow the same dataset to be analyzed in multiple ways depending on the business question. By adjusting dimensions such as category, subcategory, or store, it becomes possible to quickly evaluate sales efficiency, stock rotation, and performance differences across the network.
The examples below illustrate how the same dataset can be transformed into additional analytical views supporting deeper operational insights.



**Category Performance Overview**
![cat_resale](./images/cat_resale.png)

This pivot table presents product performance at the category and subcategory level. It combines key operational metrics such as:

- stock quantity and stock value
- total sales quantity
- weekly sales volume
- weeks of stock (WOS)
- resale rate
- weekly margin performance

This view allows quick identification of which product groups generate the strongest sales rotation relative to their stock levels.
Categories such as T-shirts and shirts or Pants and shorts show strong sales volumes and healthy resale rates, indicating stable demand and efficient stock turnover.
Meanwhile categories with higher WOS levels and lower resale rates highlight areas where inventory moves slower and may require promotional support or assortment adjustments.

**💡 Commercial insight**

Analyzing performance at the category level helps merchandising teams evaluate whether the assortment structure is balanced. Strong resale combined with low WOS typically indicates well-matched product selection and healthy inventory rotation.


**Store Performance Overview**

![store_resale](./images/store_resale.png)

This pivot table analyzes operational performance across the store network.

It compares key indicators such as:

- total stock levels
- sales quantity
- weekly sales activity
- stock coverage (WOS)
- resale performance
- weekly margin

This perspective helps identify differences in store productivity and stock efficiency.

Some stores demonstrate stronger resale rates and faster stock rotation, while others maintain higher stock levels relative to sales volume. These variations often reflect differences in:

• store size and traffic
• local demand patterns
• assortment allocation
• promotional activity

**💡 Commercial insight**

Store level analysis allows the company to identify high-performing locations as well as stores where stock levels may be disproportionate to sales potential. This type of insight supports more precise stock allocation and helps optimize inventory distribution across the network.




**Analytical Flexibility**

One of the key advantages of pivot tables is the ability to restructure the same dataset into multiple analytical perspectives.

Depending on business needs, the analysis can be quickly extended to explore:

- product category performance
- store network efficiency
- stock coverage and inventory health
- margin development across product groups
- promotional product impact on sales

The richer the dataset, the more detailed and insightful these analytical views can become. This flexibility makes pivot tables a powerful tool for exploratory business analysis and rapid operational diagnostics.



## **📌Final Business Summary**

The analysis of sales performance, stock levels and product structure reveals several important operational trends across the assortment.

The company's strategy for the current season clearly focused on reducing excess inventory while improving product mix quality. Compared to the previous year, total inventory levels decreased significantly, while overall sales performance remained relatively stable. This indicates that the previous stock levels were likely higher than required and that the assortment has become more efficient.

The Current Season assortment (STD + EXC) remains the primary driver of business performance. Despite lower inventory levels, sales volumes remained relatively stable, which suggests that demand is being met with a more optimized product structure.

The EXC assortment played a particularly important role in driving weekly sales performance. Promotional and licensed products generated strong sales dynamics, supporting overall revenue despite lower inventory levels.

The STD assortment, which represents the core product offering, experienced lower stock levels and slightly lower sales volumes. However, margin levels remained relatively stable, indicating that the core assortment continues to perform consistently.

The Country assortment acts as a complementary supply source supporting the main assortment. Strong sales growth in selected categories indicates that locally sourced products successfully filled assortment gaps and supported overall sales performance.

Finally, the OLD assortment shows a significant reduction in stock levels, confirming that the company has been actively clearing legacy inventory from previous seasons. This is an important step toward improving overall stock health and reducing long-term inventory risk.

Overall, the results suggest that the company successfully improved inventory efficiency, stock rotation and assortment quality, even though total sales value slightly declined due to pricing adjustments and promotional activity.




## **🚀 Future Business Opportunities**

Based on the results of the analysis, several opportunities for further business and analytical development can be identified.

**Inventory optimization**

The analysis confirms that the significant reduction of stock levels did not lead to a proportional decline in sales performance. This indicates that previous inventory levels were likely higher than required.

Further improvements in stock allocation across stores could help maintain product availability while continuing to optimize inventory efficiency. Better alignment between demand patterns and stock distribution would support healthier stock rotation and reduce the risk of overstocking.

**Assortment management**

The results suggest that product selection and collection structure play a more important role than absolute stock volume.

Some categories achieved stable sales results despite lower inventory levels, which indicates that a well-selected assortment can perform efficiently even with reduced stock. This highlights the importance of focusing more strongly on model-level assortment decisions within each category, rather than increasing total stock volume.

For buyers and traders, this means that greater attention should be given to product selection, collection structure and demand alignment, ensuring that the right products are introduced at the right time in the season.

**Promotional and licensing strategy**

The EXC assortment demonstrated strong sales dynamics, confirming that promotional and licensed products can play an important role in stimulating demand.

A more structured approach to promotional planning could help leverage these products more effectively throughout the season. Aligning promotional activity with demand cycles and product availability may improve both sales performance and stock rotation.

**Store level performance optimization**

The store-level analysis revealed noticeable differences in resale rates, stock coverage and sales productivity across the network.

Further exploration of these patterns could support more precise store segmentation and allow the company to allocate assortment and inventory more effectively depending on store performance, local demand and sales capacity.

**Advanced analytics and reporting integration**

Future analytical development could involve integrating this dataset into interactive BI tools such as Power BI or Tableau.

By connecting sales, stock and supply data through relational data models, it would be possible to create a more comprehensive analytical environment combining:

- sales performance
- stock levels
- delivery volumes
- product assortment structure

Analyzing deliveries across weekly, monthly and yearly time horizons would provide additional insight into how supply flows influence stock levels and sales performance.

Such an integrated analytical approach would support more informed operational decisions and allow the business to move toward a more data-driven inventory and assortment management strategy.


## **📈 Key Analytical Insights**

The analysis revealed several important patterns regarding sales performance, assortment structure and inventory management across the retail network.

**Inventory reduction did not significantly impact sales**

One of the most important findings is that the company significantly reduced inventory levels while maintaining relatively stable sales performance.

Total stock quantity decreased by approximately 24%, while total sales quantity declined by only 3%. This suggests that previous stock levels were higher than necessary and that the assortment is now operating with a healthier inventory structure.

This confirms that inventory optimization can improve operational efficiency without negatively impacting demand fulfillment.

**Promotional assortment played a key role in sales dynamics**

The EXC assortment, which includes promotional and licensed products, showed strong growth dynamics compared to the previous year.

Weekly sales quantity increased significantly and contributed to maintaining overall sales performance despite lower inventory levels. This indicates that promotional products were effectively used as a demand-generation mechanism during the season.

These results highlight the importance of strategic promotional assortment planning in driving short-term sales performance.

**Assortment quality proved more important than stock volume**

Another key insight is that collection structure and product selection appear to be more critical than total stock levels.

Several product categories maintained stable sales performance despite reduced inventory, suggesting that better assortment planning allowed the company to focus on higher-performing product models.

This reinforces the importance of data-driven assortment decisions at the model level, where buyers and traders select products based on demand potential rather than increasing overall inventory volume.

**Store level analysis highlights opportunities for allocation improvements**

Analysis of individual stores revealed noticeable differences in resale rates, stock coverage and sales productivity.

Some stores achieved significantly higher resale performance with lower stock coverage, suggesting more efficient stock rotation. This indicates that further improvements in store-specific assortment allocation and inventory distribution could enhance overall network performance.

Better alignment between local demand patterns and product allocation may help increase sales productivity while maintaining optimized stock levels.







**This project demonstrates how retail sales data can be transformed into actionable business insights using Excel-based analytical workflows.**





