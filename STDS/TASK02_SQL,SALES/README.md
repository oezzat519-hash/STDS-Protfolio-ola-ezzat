
1️⃣ AdventureWorksLT Sales — SQL Data Preparation & Excel Dashboard 🗄️

This project demonstrates a full SQL data cleaning, consolidation, and Excel reporting workflow using the AdventureWorksLT2022 database.

🔹 Steps Performed

📝 Profiled raw SalesLT tables

🧹 Created cleaned tables: Address, Customer, CustomerAddress, Product, ProductCategory, ProductModel, ProductModelProductDescription, SalesOrderHeader, SalesOrderDetail

📆 Engineered date attributes (day, month, year)

🔗 Merged all tables into a single table: Merged_SalesData

💾 Exported to Excel for PivotTables and dashboards

📂 Tables Processed

SalesLT.Address → Clean_Address

SalesLT.Customer → Clean_Customer

SalesLT.CustomerAddress → Clean_CustomerAddress

SalesLT.Product → Clean_Product

SalesLT.ProductCategory → Clean_ProductCategory

SalesLT.ProductModel → Clean_ProductModel

SalesLT.ProductModelProductDescription → Clean_ProductModelProductDescription

SalesLT.SalesOrderHeader → Clean_SalesOrderHeader

SalesLT.SalesOrderDetail → Clean_SalesOrderDetail

These tables were transformed into dbo.Clean_* versions using SELECT ... INTO.

🔹 Key Cleaning Examples

Address → Clean_Address: kept AddressID, AddressLine1, City, StateProvince, CountryRegion, PostalCode; handled nulls and duplicates

Customer → Clean_Customer: retained CustomerID, CompanyName, SalesPerson, with null/duplicate checks

Product → Clean_Product: preserved pricing and category links; added SellStartDay/Month/Year

SalesOrderHeader → Clean_SalesOrderHeader: derived day/month/year for Order, Due, Ship dates

🔗 Final Merge — Merged_SalesData

All cleaned tables were left-joined to create a single analytics table:

SELECT  
    soh.SalesOrderID, soh.Status, soh.OnlineOrderFlag, soh.SalesOrderNumber, soh.PurchaseOrderNumber,
    soh.AccountNumber, 
    c.CustomerID, c.CompanyName,
    a_ship.AddressLine1 AS ShipAddress, a_ship.City AS ShipCity, a_ship.StateProvince AS ShipState, a_ship.PostalCode AS ShipPostalCode,
    a_bill.AddressLine1 AS BillAddress, a_bill.City AS BillCity, a_bill.StateProvince AS BillState, a_bill.PostalCode AS BillPostalCode,
    sod.SalesOrderDetailID, sod.OrderQty, sod.UnitPrice, sod.UnitPriceDiscount, sod.LineTotal,
    p.ProductID, p.Name AS ProductName, p.StandardCost, p.ListPrice,
    pc.Name AS ProductCategory, pm.Name AS ProductModel, pmpd.Culture AS ProductDescription
INTO Merged_SalesData
FROM dbo.Clean_SalesOrderHeader AS soh
LEFT JOIN dbo.Clean_Customer AS c ON soh.CustomerID = c.CustomerID
LEFT JOIN dbo.Clean_CustomerAddress AS ca_ship ON soh.ShipToAddressID = ca_ship.AddressID AND soh.CustomerID = ca_ship.CustomerID
LEFT JOIN dbo.Clean_Address AS a_ship ON ca_ship.AddressID = a_ship.AddressID
LEFT JOIN dbo.Clean_CustomerAddress AS ca_bill ON soh.BillToAddressID = ca_bill.AddressID AND soh.CustomerID = ca_bill.CustomerID
LEFT JOIN dbo.Clean_Address AS a_bill ON ca_bill.AddressID = a_bill.AddressID
LEFT JOIN dbo.Clean_SalesOrderDetail AS sod ON soh.SalesOrderID = sod.SalesOrderID
LEFT JOIN dbo.Clean_Product AS p ON sod.ProductID = p.ProductID
LEFT JOIN dbo.Clean_ProductCategory AS pc ON p.ProductCategoryID = pc.ProductCategoryID
LEFT JOIN dbo.Clean_ProductModel AS pm ON p.ProductModelID = pm.ProductModelID
LEFT JOIN dbo.Clean_ProductModelProductDescription AS pmpd ON p.ProductModelID = pmpd.ProductModelID;

📊 Excel Analytics & Dashboard

After SQL cleaning, the data was exported to Excel to create a professional reporting tool.

📈 Excel Workbook Layout

🗃️ Sales_Data: Clean flat dataset from SQL

📑 Pivots: PivotTables for Net Sales by Category and key metrics

🎛️ Dashboard: High-level interactive dashboard with KPIs and slicers

🛠 Tools & Skills
Tool	Skills Demonstrated
SQL Server (T-SQL)	Data profiling, cleaning, SELECT INTO, complex joins
Microsoft Excel	PivotTables, calculated fields, interactive dashboards, data visualization
📦 Deliverables

📝 Sales_SQLQuery1.sql — Full SQL pipeline script

💾 sales_sqldata(version1).xlsb(1).xlsx — Final Excel workbook

 Dashboard Preview — Interactive visual interface

📝 Reflection
💡 Key Learnings

Mastered data consolidation techniques

Learned that raw data requires structured SQL cleaning pipelines before analysis
=======================================================================================================================
⚠️ Challenges

    -Managing multiple joins between Shipping and Billing addresses without duplicates required careful LEFT JOIN logic
=======================================================================================================================
🚀 Improvements

   -Improved documentation skills

   -Learned to transition data smoothly from SQL to business-friendly Excel dashboards