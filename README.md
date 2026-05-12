# FMCG Manufacturing, Pricing & Profitability Analytics System

A full-scale SQL Server + Power BI analytics platform designed for FMCG manufacturing operations, pricing intelligence, capacity planning, and profitability analysis.

This project centralizes production, operational cost, pricing ladder, taxation, and plant-level KPI analytics into a single governed reporting system for management and operational decision-making.

---

## Project Overview

The system was built to solve key manufacturing and pricing challenges in an FMCG environment by integrating:

- Manufacturing capacity analytics
- Cost computation models
- Pricing ladder automation
- Tax calculation logic (Pre-GST & GST)
- Profitability analytics
- Power BI reporting & KPI monitoring

The platform acts as a **single source of truth** for production and pricing analytics across manufacturing plants. :contentReference[oaicite:0]{index=0}

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

:contentReference[oaicite:1]{index=1}

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
### `FACT_PRD_MANU_PROD_MASTER_MAIN_NEW_DATA`

Contains:
- Daily production quantities
- Production capacities
- Operational costs
- Pack sizes
- Manufacturing dates
- Product/category information

:contentReference[oaicite:2]{index=2}

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

:contentReference[oaicite:3]{index=3}

---

# Core Business Logic

## Unit Conversion Logic

```sql
1 Quintal = 100 KG
1 KG = 1000 grams/ml
1 Quintal = 100,000 grams/ml
