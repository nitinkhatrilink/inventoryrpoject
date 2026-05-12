# FMCG Manufacturing, Pricing & Profitability Analytics System

A full-scale SQL Server + Power BI analytics platform designed for FMCG manufacturing operations, pricing intelligence, capacity planning, and profitability analysis.

This project centralizes production, operational cost, pricing ladder, taxation, and plant-level KPI analytics into a single governed reporting system for management and operational decision-making.

---

# Project Overview

The system was built to solve key manufacturing and pricing challenges in an FMCG environment by integrating:

- Manufacturing capacity analytics
- Cost computation models
- Pricing ladder automation
- Tax calculation logic (Pre-GST & GST)
- Profitability analytics
- Power BI reporting & KPI monitoring

The platform acts as a single source of truth for production and pricing analytics across manufacturing plants.

---

# Business Problems Solved

| Problem | Solution |
|---|---|
| No visibility into plant utilization | Capacity utilization KPIs |
| Manual pricing calculations | Automated pricing ladder |
| Inconsistent margin calculations | Category-based pricing rules |
| No profitability visibility | Profit per pack & profit analysis |
| No historical tax handling | Pre-GST vs GST tax engine |
| Difficult scenario analysis | Produced vs Installed vs Target comparisons |

---

# Tech Stack

## Data Layer
- SQL Server
- T-SQL
- CTEs
- Views
- Window Functions
- Joins

## BI & Visualization
- Power BI
- DAX
- Power Query
- KPI Dashboards

## Analytics Areas
- Manufacturing Analytics
- Pricing Analytics
- Cost Analytics
- Profitability Analytics
- Supply Chain Analytics

---

# Data Model

## Fact Table

### FACT_PRD_MANU_PROD_MASTER_MAIN_NEW_DATA

Contains:
- Daily production quantities
- Production capacities
- Operational costs
- Pack sizes
- Manufacturing dates
- Product/category information

---

## Dimension Tables

| Table | Purpose |
|---|---|
| DM_Manufacturing_Unit | Plant details |
| DM_State | State mapping |
| DM_Material_Category | Raw material grouping |
| DM_Category | Product category |
| DM_Subcategory | Product subcategory |
| DM_Plant_Manager | Plant ownership |
| DM_Product_Pack | Packaging details |

---

# Core Business Logic

## Unit Conversion Logic

```sql
1 Quintal = 100 KG
1 KG = 1000 grams/ml
1 Quintal = 100,000 grams/ml
```

Used for converting production quantities into retail-ready packs.

---

## Packs Per Quintal

```sql
PacksPerQuintal = 100000 / PackSize_Value
```

Calculates how many retail packs can be produced from one quintal.

---

## Total Retail Packs Produced

```sql
TotalRetailPacksProduced =
ProducedCapacityQuintalbyDay * PacksPerQuintal
```

Converts manufacturing output into consumer-ready retail packs.

---

# Manufacturing KPIs

## Capacity Utilization

```sql
Capacity Utilization % =
ProducedCapacityQuintalbyDay /
ProductionCapacityQuintalbyDay * 100
```

### Utilization Classification

| Range | Status |
|---|---|
| < 80% | Under Utilization |
| 80–99% | Optimal |
| 100% | Fully Utilized |

---

# Costing Engine

## Total Operational Cost

```sql
TotalOperationalCost =
PlantCost + MaintenanceCostbyday
```

## Base Cost Per Pack

```sql
BaseCostPerPack =
TotalOperationalCost / TotalRetailPacksProduced
```

Variants:
- ProducedBaseCostPerPack
- ProductionBaseCostPerPack
- TargetBaseCostPerPack

---

# Pricing Engine

The project implements a full FMCG pricing ladder:

```text
Base Cost
→ Ex-Factory Price
→ Wholesale Price
→ Pre-Tax MRP
→ Final MRP
→ Net Selling Price
→ Profit Per Pack
```

---

## Margin Logic

### Manufacturer Margin

| Category | Margin |
|---|---|
| Beverages | 25% |
| Food | 20% |

### Distributor Margin

| Category | Margin |
|---|---|
| Beverages | 10% |
| Snacks | 10% |
| Biscuits | 7% |
| Breakfast | 9% |

### Retailer Margin

| Category | Margin |
|---|---|
| Beverages | 20% |
| Snacks | 22% |
| Biscuits | 18% |
| Breakfast | 15% |

---

# Tax Engine

The project dynamically handles both:

- Pre-GST taxation
- GST taxation

## GST Logic

### Before July 2017
- Food → VAT 5%
- Beverages → VAT 12.5%

### After July 2017
- Food → GST 12%
- Beverages → GST 18%

---

# Profitability Metrics

## Profit Per Pack

```sql
ProfitPerPack =
NetSellingPrice - BaseCostPerPack
```

Variants:
- ProfitPerPack_Produced
- ProfitPerPack_Production
- ProfitPerPack_Expected

---

# Advanced SQL Concepts Used

- Complex CTE chaining
- Analytical views
- Window functions
- Partition-based calculations
- Aggregations
- Scenario modeling
- Dynamic pricing logic
- Conditional tax handling

Example:

```sql
AVG(ProducedCapacityQuintalbyDay)
OVER (PARTITION BY Year, Month)
```

---

# Final SQL Output

## Analytical View

```sql
VW_FMCG_MANUFACTURING_PRICING_ANALYTICS
```

Contains:
- Manufacturing KPIs
- Capacity utilization
- Cost metrics
- Pricing calculations
- MRP calculations
- Profitability analytics
- Scenario comparison metrics

---

# Power BI Dashboards

The reporting layer includes:

- Manufacturing Overview
- Plant Efficiency Dashboard
- Cost & Pricing Waterfall
- Category Profitability
- Utilization vs Profit Analysis
- Historical Tax Comparison
- State-wise Performance
- Plant Manager Performance

---

# Key Features

- Enterprise-style SQL analytical layer
- Automated FMCG pricing engine
- Dynamic tax logic
- Pack-size aware calculations
- Capacity utilization analytics
- Scenario comparison modeling
- KPI-driven dashboards
- Profitability tracking
- Multi-level manufacturing analysis

---

# Business Impact

- Improved pricing accuracy
- Centralized operational reporting
- Enabled profitability visibility
- Identified under-utilized plants
- Improved cost transparency
- Reduced manual calculations
- Standardized manufacturing KPIs

---

# Sample KPIs

| KPI | Description |
|---|---|
| Capacity Utilization % | Plant efficiency |
| Cost per Pack | Manufacturing cost efficiency |
| Profit per Pack | Product profitability |
| Maintenance % | Maintenance cost contribution |
| Energy Efficiency | Production vs fuel cost |
| Growth % | Production trend analysis |
| Variance % | Actual vs target analysis |

---

# Architecture Flow

```text
ERP / Manufacturing Data
        ↓
SQL Server Data Layer
        ↓
CTEs + Views + Business Logic
        ↓
Analytical View
        ↓
Power BI Semantic Model
        ↓
Interactive Dashboards
        ↓
Management Insights
```

---

# Learning Outcomes

Through this project, the following concepts were implemented:

- Data modeling
- SQL optimization
- Manufacturing analytics
- Pricing systems
- Cost modeling
- Business KPI design
- Power BI dashboarding
- DAX calculations
- Window functions
- Enterprise BI architecture

---

# Future Improvements

- Predictive demand forecasting
- Inventory optimization
- Procurement analytics
- Real-time production monitoring
- AI-driven pricing optimization
- Supply chain analytics

---

# Author

Nitin  
Data Analyst | Power BI Developer | BI Engineer

Technologies:
SQL Server • Power BI • DAX • Power Query • T-SQL
