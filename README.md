# Business data analysis using PowerBI

## Project overview
Provide an interactive dashboard/report for AdwentureWorks Sales Department, using PowerBI and Adewntureworks 2005 data base stored in BigQuery Project.

## About the database
AdwentureWorks is a sample database provided by Microsoft to demonstrate the features and capabilities of SQL Server. 
The AdventureWorks database includes various tables, views, and stored procedures to represent a fictional company's operations, focusing on manufacturing, sales, purchasing, and other business processes. 
It provides a realistic dataset for learning and practicing SQL queries, database design, and other database-related tasks.

The schema of AdwentureWorks 2005 database can be accessed [here]( https://drive.google.com/file/d/1-Qsnn3bg0_PYgY5kKJOUDG8xdKLvOLPK/view)

## Access to the project
The project has been uploaded in the PowerBI template and can be accessed here.

The static version of the project has been uploaded in the PDF file and can be accessed here.

## Steps applied
**Step 1:** Extracting and transforming necessary data from BigQuery

**Step 2:** Loading and transforming data in Power Query Editor

**Step 3:** Preparing data model in Star Schema for optimized performance and clarity

**Step 4:** Creating visualisations to provide comprehensive analysis of **Sales, Profit, Orders and Products**

**Step 5:** Designing the dashboard layout

**Step 6:** Adding slicers bookmarks and buttons for enhanced user experience

## Further steps recommended
**Step 7:** Publishing the report to Power BI Service

**Step 8:**  Setting up data refresh schedules to ensure the dashboard remains up-to-date

**Step 9:**  Sharing and managing access permissions for stakeholders

**Step 10:** Gathering feedback and iterating on the dashboard design for continuous improvement


## Comments to the project

### Fiscal Calendar

AdventureWorks has a different fiscal year than calendar year. Their fiscal year begins on July 1 and ends on June 30. Since for a company that uses a fiscal year other than calendar year, it is appropriate to present the data according to the fiscal year, the dashboard has been prepared to present data in accordance with the fiscal year beginning in July (Created Calculating Table with Fiscal Year, Quarter, Month)

### Timeseries analysis
Because the data for July 2004 (which in this case is also the first month of fiscal year 2005) is incomplete and its use would cause misleading results, especially in trend visualizations, this month has been filtered out at the report level. 

###  Profit data
AdwentyreWorks 2005 database do not contain a column/data presenting directly the Profit from operations. For the purpose of the project the Profit calculation has been derived from the available data:

SalesOrderHeader: OrderDate

Sales Order Detail: LineTotal (UnitPrice * OrderQty)

Product Cost History: StandardCost (cost per unit at different points in time),  StartDate and EndDate appropriately considered to get the correct cost at the time of sale

The SQL code applied for this purpose can be accessed here

### Sales data
For the purpose of a more comprehensive analysis, the Sales value is calculated using the LineTotal column from SalesOrderDetail instead of the TotalDue column from SalesOrderHeader.

The LineTotal column represents the total amount for a line item in a sales order.

LineTotal = (UnitPrice × OrderQty) − (UnitPrice × OrderQty × UnitPriceDiscount)

The TotalDue column represents the total amount due for the entire sales order, which includes the sum of all line items (sum of LineTotal) and additional charges such as taxes and shipping fees.

TotalDue = SubTotal + TaxAmt + Freight

Therefore, the SalesOrderHeader and SalesOrderDetail tables have different levels of granularity (levels of detail). The SalesOrderHeader table captures data at a higher level of granularity, representing the overall details of a sales order. Each record in this table corresponds to a single sales order. The SalesOrderDetail table captures data at a finer level of granularity, representing individual line items within a sales order. Each record in this table corresponds to a single product line item in a sales order.

In this context, using LineTotal from SalesOrderDetail allows for a more in-depth analysis, as it can be analyzed by additional dimensions like Category, Subcategory, and Product.

In the context of this project, sales are therefore understood as the sales amount before applying tax and freight fees. 
