# SwiftLog Logistics Supply Chain Analytics & Business Intelligence

## Project Overview

This project was completed as part of the **AnalystLab Africa Experience Lab Internship Programme – Week 5 Data Analytics Track**.

The objective was to develop an end-to-end **Business Intelligence solution in Power BI** for **SwiftLog Logistics Limited**, using logistics datasets covering customers, orders, products, inventory, warehouses, shipments, delivery performance, employees, suppliers, and returns.

The solution transforms operational data into actionable insights that support management decision-making in areas such as:

- Revenue and order performance
- Customer analysis
- Inventory management
- Warehouse performance
- Shipment and delivery efficiency
- Product performance
- Returns monitoring
- Executive KPI tracking

---

## Business Objectives

The Power BI solution was designed to help SwiftLog management:

- Monitor overall business performance
- Improve delivery efficiency
- Reduce operational inefficiencies
- Improve inventory management
- Evaluate warehouse performance
- Monitor customer and product performance
- Reduce product returns
- Support data-driven executive decision-making

---

## Tools Used

- **Power BI Desktop**
- **Power Query**
- **DAX**
- **Excel / CSV**
- **GitHub**

---

## Datasets Used

- `SwiftLog_Customers.csv`
- `SwiftLog_Orders.csv`
- `SwiftLog_Order_Items.csv`
- `SwiftLog_Products.csv`
- `SwiftLog_Inventory.csv`
- `SwiftLog_Warehouses.csv`
- `SwiftLog_Shipments.csv`
- `SwiftLog_Delivery_Performance.csv`
- `SwiftLog_Employees.csv`
- `SwiftLog_Suppliers.csv`
- `SwiftLog_Returns.csv`
- `SwiftLog_Data_Dictionary.xlsx`

---

## Data Preparation & Cleaning

Data preparation was completed in Power Query before model development.

Key steps included:

- Inspecting all datasets
- Verifying column names and data types
- Checking primary and foreign keys
- Checking for missing values
- Checking for duplicate records
- Standardizing text values using Trim and Clean
- Correcting data types
- Removing exact duplicate inventory records
- Grouping employee records by warehouse
- Merging employee counts into the Warehouses table
- Merging Delivery Performance into the Shipments table
- Creating a dedicated Date table
- Creating Month, Month Number, and Quarter fields
- Creating business fields such as Stock Status
- Optimizing the model to support analysis and reporting

### Data Quality Note

Three exact duplicate rows were identified and removed from the Inventory dataset, leaving **3,997 rows**.

---

## Data Model

The Power BI model uses a relational structure connecting the main operational datasets.

Key relationships include:

- Customers → Orders
- Orders → Order Items
- Products → Order Items
- Products → Inventory
- Warehouses → Inventory
- Warehouses → Shipments
- Orders → Shipments
- Orders → Returns
- DateTable → Orders

Single-direction filtering was used where possible.

### Important Modeling Limitation

The **Suppliers** table does not contain a usable relationship to Products, Shipments, or Inventory because no shared `SupplierID` key exists in those datasets.

For this reason, supplier performance was not calculated using unsupported assumptions.

---

## Key DAX Measures

The report contains more than 10 custom DAX measures, including:

- Total Revenue
- Total Orders
- Total Customers
- Total Products
- Total Shipments
- Average Order Value
- Average Delivery Delay
- Inventory Stock Level
- Inventory Turnover Proxy
- Return Rate
- On-Time Delivery Rate
- Delayed Shipments
- Low Stock Products
- Units Ordered
- Total Warehouses
- Selected Product

### Example

```DAX
Total Revenue =
SUMX(
    SwiftLog_Order_Items,
    SwiftLog_Order_Items[Quantity] *
    RELATED(SwiftLog_Products[UnitPrice])
)
```

---

## Dashboard Pages

### 1. Executive Dashboard

Provides a high-level overview of:

- Total Revenue
- Total Orders
- Average Order Value
- Average Delivery Delay
- On-Time Delivery Rate
- Return Rate
- Revenue trends
- Order trends
- Delivery performance
- Executive filters

### 2. Executive Trends

Focuses on:

- Monthly revenue
- Monthly orders
- Delivery status
- Return overview
- Return reasons
- Dynamic report title

### 3. Customer Analytics

Includes:

- Total Customers
- Customers by City
- Customer Growth Trend
- Top Customers by Revenue
- Customer Order Frequency

### 4. Inventory & Warehouse Analytics

Includes:

- Inventory Stock Level
- Low Stock Products
- Total Warehouses
- Inventory by Warehouse
- Warehouse comparison
- Inventory Turnover Proxy
- Inventory by Product Category

### 5. Shipment & Delivery Analytics

Includes:

- Total Shipments
- Delayed Shipments
- Average Delivery Delay
- On-Time Delivery Rate
- Delivery Status
- Delivery performance by location
- Monthly Shipment Trend
- Delayed Shipments by Warehouse

### 6. Product & Supplier Analytics

Includes:

- Total Products
- Revenue by Product Category
- Top Products by Revenue
- Best-Selling Products
- Returns by Reason
- Supplier data limitation note

### Additional Pages

- Product Details Drill-through
- Product Tooltip

---

## Advanced Power BI Features

The project includes:

- Drill-through pages
- Bookmarks
- Dynamic tooltips
- Page navigation buttons
- Slicers
- Synchronized Month slicer
- Cross-filtering visuals
- Dynamic report titles
- Conditional formatting
- Advanced DAX measures
- Mobile report layouts
- Professional dashboard theme and layout

A What-If parameter was not added because the project guide specified it only **where appropriate**, and the available data did not justify forcing an artificial scenario into the model.

---

## Key Findings

### Revenue & Product Performance

- Total Revenue: approximately **7.11M**
- Fashion generated approximately **2.73M (38.38%)**
- Food generated approximately **2.37M (33.33%)**
- Electronics generated approximately **2.01M (28.29%)**
- Top revenue products included **P203, P085, and P229**

### Customer Performance

Top revenue-generating customers included:

- Customer 223
- Customer 773
- Customer 599

### Delivery Performance

Delivery performance was the most urgent operational issue identified.

- Total Shipments: **5,000**
- Delayed Shipments: **3,186**
- Delayed shipment share: approximately **63.72%**
- On-Time Delivery Rate: **37.21%**
- Average Delivery Delay: **3.52 days**

### Regional Delivery Delays

- Lagos: **1,701 delayed shipments**
- Abuja: **849 delayed shipments**
- Kano: **636 delayed shipments**

Lagos had the largest absolute delivery-delay burden.

### Inventory & Warehouses

- Total Warehouses: **15**
- Low Stock Products: **186**
- W13 showed comparatively lower delayed shipment volume based on the available delivery indicator

### Peak Business Activity

- **August** recorded the highest activity:
  - approximately **654 orders**
  - approximately **2.85M revenue**
- April was also strong:
  - approximately **638 orders**
  - approximately **2.74M revenue**

> September data is incomplete and only covers activity through 8 September 2026.

---

## Data Limitations

Several important limitations were identified and documented instead of making unsupported calculations.

### Supplier Performance

Supplier performance cannot be reliably calculated because the Suppliers table is not linked to Products, Inventory, or Shipments through a common `SupplierID`.

### Product Return Rate

The Returns dataset contains `OrderID` but does not contain `ProductID` or `OrderItemID`. Many returned orders contain multiple products, so product-level return rates cannot be attributed reliably.

### Average Delivery Time

Average delivery time cannot be calculated because shipment and delivery timestamps are not available.

### Warehouse Utilization

A formal warehouse utilization rate cannot be calculated because warehouse capacity data is not available.

### Inventory Turnover

A formal financial inventory turnover ratio cannot be calculated because Cost of Goods Sold and average inventory value are not available. The dashboard therefore uses an **Inventory Turnover Proxy** based on available operational data.

---

## Strategic Recommendations

1. Improve on-time delivery performance through route, dispatch, and delay root-cause analysis.
2. Prioritize operational improvements in Lagos because it has the highest delayed shipment volume.
3. Benchmark lower-delay warehouses and replicate effective operating practices.
4. Protect availability of high-revenue products such as P203, P085, and P229.
5. Develop retention strategies for high-value customers.
6. Prepare stock, staffing, and transport capacity ahead of peak demand periods.
7. Improve inventory balancing across warehouses using low-stock and demand indicators.
8. Reduce avoidable returns by addressing damaged items, wrong items, and late deliveries.
9. Strengthen source-data design by adding supplier, product-return, delivery-time, and warehouse-capacity fields.
10. Establish continuous KPI monitoring through the Power BI dashboards.

---

## Repository Structure

```text
Week5_DataAnalytics_SwiftLog/
│
├── Data/
│   └── Original_Datasets/
│
├── Dashboard/
│   └── SwiftLog_Analytics.pbix
│
├── Report/
│   ├── Executive_BI_Report.pdf
│   ├── Dashboard_Screenshots.pdf
│   └── SwiftLog_Technical_Project_Documentation.pdf
│
├── Presentation/
│   └── SwiftLog_Executive_Presentation.pptx
│
├── Images/
│   ├── Executive_Dashboard.png
│   ├── Data_Model_View.png
│   ├── Power_Query_Cleaning.png
│   ├── DAX_Measures.png
│   └── Dashboard_Montage.png
│
├── References/
│   ├── AnalystLab_Africa_Week5_Assignment.pdf
│   ├──Calculated_Fields_Data_Dictionary.csv
|   ├──SwiftLog_Data_Dictionary.xlsx
│   └── References.md
│
└── README.md
```

---

## How to View the Project

1. Download or clone this repository.
2. Open `Dashboard/SwiftLog_Analytics.pbix` using Power BI Desktop.
3. Use the page navigation buttons to move between dashboards.
4. Use slicers to filter the report.
5. Right-click supported product visuals to access the Product Details drill-through page.
6. Hover over supported product visuals to view the Product Tooltip.
7. Review the PDF report and presentation for executive-level findings and recommendations.

---

## Deliverables

This repository contains the core deliverables for the Week 5 Data Analytics project:

- Power BI dashboard
- Executive BI Report
- Technical Project Documentation
- Dashboard Screenshots
- Executive Presentation
- Data Dictionary for calculated fields
- Supporting images
- Project references
- README documentation

---

## Project Preview

### Data Model View

![Data Model View](Images/Data%20Model%20View.png)

## Acknowledgement

Project brief provided by **AnalystLab Africa** as part of the Week 5 Experience Lab Internship Programme.

**#AnalystLabAfrica**
