🗄️ SQL Data Cleaning & Analytics Dataset — AdventureWorksLT Sales

🎯 Objective

   -Prepare an analytics-ready sales dataset by cleaning and consolidating multiple AdventureWorksLT2022 tables. The goal   is to generate a single wide table (Merged_SalesData) suitable for BI tools and Excel PivotTables.
==========================================================================================================================
🗂 Source System

  -Database: AdventureWorksLT2022 (SalesLT schema)

  -Tables Used:

    *Address
    *Customer
    *CustomerAddress
    *Product
    *ProductCategory
    *ProductModel
    *ProductModelProductDescription
    *SalesOrderHeader
    *SalesOrderDetail
==========================================================================================================================
🧹 Data Preparation Steps

   -Column & Data Profiling
   -Inspected columns and data types using INFORMATION_SCHEMA.COLUMNS.
   -Row Counts & Data Previews
   -Checked table sizes and sampled data to understand structure.
==========================================================================================================================
🧹 Clean Tables (dbo.Clean_*)

  -Created with SELECT ... INTO including only essential columns:
  -Clean_Address, Clean_Customer, Clean_CustomerAddress
  -Clean_Product, Clean_ProductCategory, Clean_ProductModel, Clean_ProductModelProductDescription
  -Clean_SalesOrderHeader, Clean_SalesOrderDetail
  -Null & Duplicate Checks
  -Ensured data integrity using SUM(CASE WHEN ...) and GROUP BY HAVING COUNT
==========================================================================================================================
📆 Date Engineering

   -Clean_Product: added SellStartDay/Month/Year (optionally removed original date).
   -Clean_SalesOrderHeader: added OrderDay/Month/Year, DueDay/Month/Year, ShipDay/Month/Year; removed original columns after extraction.
==========================================================================================================================
🔗 Merge Cleaned Tables

  -Combined all cleaned tables into Merged_SalesData using LEFT JOINs across Header, Detail, Customer, Address, Product,      Category, Model, Description.
==========================================================================================================================
💾 Output & Analysis

   -Exported Dataset: Merged_SalesData → Excel file: sales_sqldata (version 1).xlsb (1).xlsx
   -Excel Workbook Structure
   -sales_sqldata Sheet: Flat dataset including Order, Customer, Location, Product, Category, Pricing, Net Sales
   -Pivots Sheet: Summary tables such as:
     *Sum of Net Sales
     *Count of SalesOrderID
     *Average Order Value (AOV)
   -Total Orders by Category / City / Region
   -Dashboard Sheet: Interactive visuals and KPIs
=========================================================================================================================
📝 Deliverables

  -SQL Script: Sales_SQLQuery1.sql (data cleaning + merging)
  -Exported Dataset: Sales_Export.csv (optional)
  -Excel Analysis: sales_sqldata (version 1).xlsb (1).xlsx (pivots + dashboard)
=========================================================================================================================

✅ Acceptance Criteria

  -Clean Tables: Exist with correct primary/foreign keys and minimal nulls/duplicates.
  -Merged_SalesData: Includes all relevant fields from Header, Detail, Customer, Address, Product, and Category.
  -Excel Analysis: Accurately aggregates Net Sales, Order Counts, and provides breakdowns by Category and Location.
