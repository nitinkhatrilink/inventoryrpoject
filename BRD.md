# Business Requirement Document (BRD)

## FMCG Manufacturing Analytics Platform

This document defines the business requirements, analytical objectives, KPI definitions, data model expectations, and reporting requirements for the FMCG Manufacturing & Pricing Analytics Platform.

The project was designed to build a centralized analytics system for monitoring manufacturing operations, production efficiency, costing, pricing, and profitability across multiple FMCG manufacturing units.

---

# Project Background

CoolBev Foods Pvt. Ltd. manufactures food and beverage products across multiple manufacturing plants.

The business required a centralized analytics platform to:

- Monitor production output
- Track plant utilization
- Analyze operational costs
- Standardize pricing calculations
- Improve profitability visibility
- Build management-level KPI dashboards

The organization lacked a governed reporting system and relied heavily on fragmented operational reporting.

---

# Project Goal

To build an enterprise-grade SQL Server + Power BI analytics solution capable of:

- Centralizing manufacturing analytics
- Automating pricing calculations
- Standardizing KPIs
- Enabling profitability analysis
- Supporting management decision-making

---

# Business Objectives

The project focuses on solving the following business requirements:

- Track production across manufacturing plants
- Monitor plant efficiency & utilization
- Calculate cost per pack and cost per production unit
- Standardize pricing ladder calculations
- Compare target vs actual production
- Monitor operational expenses
- Enable category-wise profitability analysis
- Build historical tax-aware pricing models
- Create a single source of truth for reporting

---

# Core Business Questions

The analytics platform answers key business questions such as:

- Which plants are under-utilized?
- What is the actual production output?
- What is the cost per pack?
- Which product categories are most profitable?
- How does operational cost impact pricing?
- What is the impact of GST vs pre-GST taxation?
- Which regions contribute the highest production volume?
- How efficient are manufacturing operations over time?

---

# Core Deliverables

The project deliverables include:

## SQL Layer
- Manufacturing fact tables
- Procurement fact tables
- Dimension tables
- Analytical views
- Pricing engine calculations
- KPI calculation layer

## Power BI Layer
- Manufacturing dashboards
- Cost analysis reports
- Pricing analytics dashboards
- Profitability reports
- Executive KPI dashboards

---

# Fact Table Requirements

## FACT_MANUFACTURING

Required metrics:

- Production Capacity
- Produced Capacity
- Expected Capacity
- Pack Size
- Product Category
- Manufacturing Date
- Plant Costs
- Labor Costs
- Maintenance Costs
- Power & Fuel Costs
- Operational Charges

---

# Procurement Requirements

## FACT_PROCUREMENT

Required metrics:

- Procurement Lead Time
- Supplier Performance
- Material Cost
- Procurement Cost
- Quality Score
- Delivery Status

---

# Dimension Tables

| Dimension | Purpose |
|---|---|
| Dim_Manufacturing_Unit | Plant details |
| Dim_State | Regional mapping |
| Dim_Category | Product categories |
| Dim_SubCategory | Product hierarchy |
| Dim_Product_Pack | Packaging details |
| Dim_Material_Category | Raw material grouping |
| Dim_Plant_Manager | Ownership hierarchy |

---

# Manufacturing KPIs

## Production KPIs
- Total Production
- Capacity Utilization %
- Expected vs Actual Production
- Plant Efficiency Index
- Downtime Hours

## Cost KPIs
- Total Operational Cost
- Cost per Ton
- Cost per Pack
- Maintenance %
- Labor vs Power Cost Ratio

## Packaging KPIs
- Packs Per Quintal
- Total Retail Packs Produced
- Packaging Utilization %

## Profitability KPIs
- Profit per Pack
- Gross Profit
- Gross Margin %
- Operational Margin %

---

# Pricing Engine Requirements

The project implements a complete FMCG pricing ladder:

```text
Base Cost
→ Ex-Factory Price
→ Wholesale Price
→ Pre-Tax MRP
→ Final MRP
→ Net Selling Price
→ Profit Per Pack
```

The pricing engine supports:

- Manufacturer margins
- Distributor margins
- Retailer margins
- Category-wise pricing rules
- Historical tax logic
- GST & Pre-GST calculations

---

# Tax Logic Requirements

## Pre-GST Era (2015–2016)
- Food products → VAT
- Beverage products → VAT + Excise

## GST Era (2017 onwards)
- Food products → GST 12%
- Beverage products → GST 18%

The pricing engine dynamically adjusts taxation logic based on manufacturing date.

---

# Unit Conversion Logic

Manufacturing quantities are stored in:

- Grams
- Millilitres
- Kilograms
- Litres
- Quintals

Core conversion assumptions:

```text
1 Quintal = 100 KG
1 KG = 1000 grams/ml
1 Quintal = 100,000 grams/ml
```

---

# Key Calculation Requirements

## Packs Per Quintal

```sql
PacksPerQuintal = 100000 / PackSize
```

## Total Retail Packs Produced

```sql
TotalRetailPacksProduced =
ProducedCapacity * PacksPerQuintal
```

## Base Cost Per Pack

```sql
BaseCostPerPack =
TotalOperationalCost / TotalRetailPacksProduced
```

## Capacity Utilization %

```sql
CapacityUtilization =
ProducedCapacity / ProductionCapacity * 100
```

---

# Power BI Reporting Requirements

## Dashboards Required

### Manufacturing Overview
- Plant production summary
- Capacity utilization
- Plant comparison

### Cost Analytics
- Cost per ton
- Cost per pack
- Cost breakdown

### Pricing Analytics
- Pricing waterfall
- Margin analysis
- MRP calculations

### Profitability Dashboard
- Profit per pack
- Gross margin
- Category profitability

### Regional Analytics
- State-wise production
- Plant-wise contribution
- Regional output heatmaps

---

# Security & Governance Requirements

The system supports role-based reporting access for:

- CEO
- Operations Head
- Finance Team
- Plant Managers
- Procurement Team
- Supervisors

Governance expectations:
- Standardized KPIs
- Controlled analytical views
- Centralized reporting
- Consistent business logic

---

# Data Architecture Flow

```text
ERP / Source Data
        ↓
SQL Server Database
        ↓
Fact & Dimension Modeling
        ↓
CTEs + Analytical Views
        ↓
Power BI Semantic Model
        ↓
Interactive Dashboards
        ↓
Management Reporting
```

---

# Analytical Features

The platform supports:

- Scenario analysis
- Historical trend analysis
- YoY growth tracking
- Variance analysis
- Operational benchmarking
- Cost leakage detection
- Plant performance analysis

---

# Expected Business Impact

The platform is expected to:

- Improve operational visibility
- Reduce manual reporting effort
- Standardize pricing calculations
- Improve profitability analysis
- Identify under-utilized plants
- Improve decision-making efficiency
- Enable centralized manufacturing analytics

---

# Future Scope

Potential future enhancements include:

- Forecasting models
- Inventory analytics
- Real-time production monitoring
- Procurement optimization
- Demand planning
- Predictive maintenance
- Machine learning integration

---

# Technologies Used

- SQL Server
- T-SQL
- Power BI
- DAX
- Power Query
- Analytical Views
- Window Functions
- CTEs

---
