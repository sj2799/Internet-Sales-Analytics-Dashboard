# Internet-Sales-Analytics-Dashboard
![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge)
![Excel](https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)
![Data Modeling](https://img.shields.io/badge/Data%20Modeling-6A0DAD?style=for-the-badge)
![Star Schema](https://img.shields.io/badge/Star%20Schema-F4A300?style=for-the-badge)

A Power BI project analyzing internet sales data across currencies, time periods, and customers.

**🗂 Project Overview**
This dashboard explores a real-world-style internet sales dataset loaded from Excel. It demonstrates core Power BI skills including data modeling with a star schema, building a custom DAX date table, and creating multi-page interactive reports.

**📄 Report Pages**
Page 1 — Sales Overview
* Bar Chart: Total Sales Amount broken down by Currency Name
* Bar Chart: Total Sales Amount broken down by Month (using the custom dim_Date table)

Page 2 — Customer Breakdown
* Matrix Table: Sales Amount by Customer Email Address (rows) × Currency Code (columns)
  Useful for identifying high-value customers and their preferred currencies

**🗃 Data Model**
The project follows a star schema design with one fact table and two dimension tables, plus a custom date dimension:

| Table | Description |
|---|---|
| `fact_InternetSales` | Core sales transactions — revenue, cost, quantity |
| `dim_Customer` | Customer demographics and contact info |
| `dim_Currency` | Currency codes and names |
| `dim_Date` | Custom DAX-built date dimension |

**⚙️ DAX Formulas**
* Custom Date Table (dim_Date): Built entirely in DAX using ADDCOLUMNS + CALENDAR to dynamically span the range of the sales data:

dim_Date =
ADDCOLUMNS(
    CALENDAR(MIN(fact_InternetSales[ShipDate]), MAX(fact_InternetSales[ShipDate])),
    "Year",        YEAR([Date]),
    "Month",       MONTH([Date]),
    "Month Name",  FORMAT([Date], "MMMM"),
    "Day of Week", FORMAT([Date], "DDDD"),
    "Quarter",     FORMAT([Date], "Q"),
    "YearQuarter", FORMAT([Date], "YYYY") & "/Q" & FORMAT([Date], "Q")
)

* Aggregation (implicit measure used in visuals)

Sum of SalesAmount = SUM(fact_InternetSales[SalesAmount])

**🛠 Tech Stack**
Tool/Concept || Usage
Power BI Desktop:  Report authoring and visualization
DAX:  Date table creation, calculated columns
Power Query (M):  Data loading and transformation from Excel
Excel (.xlsx):  Source data file
Star Schema:  Data model design pattern

**✨ Features & Highlights**

✅ Custom dim_Date table built with DAX instead of Power BI's default auto date/time
✅ Star schema with clearly separated fact and dimension tables
✅ Two-page report structure — overview + customer drill-down
✅ Multi-currency sales analysis
✅ Month-level time intelligence using the custom date table
✅ Customer-level pivot for granular revenue attribution

**🎓 Learning Context**
Built as part of a mini project series from the 365 Data Science Power BI course, which covers:

*Loading and transforming data with Power Query
*Building a star schema data model
*Writing DAX to create a date dimension
*Designing multi-page reports with bar charts and matrix visuals
