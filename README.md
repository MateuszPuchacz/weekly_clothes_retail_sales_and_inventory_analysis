# weekly_clothes_retail_sales_and_inventory_analysis

## 🎯 Project Goal

This project simulates the analytical workflow I currently perform in my professional role in retail sales and inventory analysis.
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

REPORT sheet contains the main automated dashboard presenting weekly stock and sales performance.
The report combines data from two pivot tables and uses VLOOKUP-based mapping together with calculated Excel metrics to build a structured reporting layer. 


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

- $B7 – category used as lookup key
- tp_cat / tp_cat2 – pivot table data sources
- C$1 – dynamic column index controlled by header values
- IFERROR – prevents lookup errors when data is missing

Numbers placed in the header rows act as column index references, allowing the same formula to populate the entire dashboard without manually adjusting column numbers.

```

**Calculated KPI Metrics**

Calculated KPI Metrics

In addition to pivot table values, several key metrics are calculated directly in Excel, including:

```
Average Purchase Price
Average Selling Price
% Resale
Weeks of Stock
Year-over-Year change (%)
Year-over-Year value difference
```
These calculations transform raw pivot outputs into business performance indicators.



