# ShopSphere Requirements Traceability Matrix

## 1. Purpose

This document converts ShopSphere's business requirements into formal analytical requirements that can be implemented and validated across the data, SQL, Python, and Power BI layers.

The objective is to maintain traceability from:

Business Need
→ Business Question
→ Requirement
→ Data
→ KPI
→ SQL
→ Python
→ Power BI
→ Business Decision

---

# 2. Requirement Priority

| Priority | Meaning |
|---|---|
| P0 | Critical business requirement |
| P1 | High-value analytical requirement |
| P2 | Supporting analytical requirement |

---

# 3. Analytical Requirements

## REQ-001 — Overall Business Performance

**Priority:** P0

### Business Question

How is ShopSphere performing overall?

### Required Data

- Orders
- Order items
- Products
- Customers
- Discounts
- Product costs
- Order status

### KPIs

- Net Revenue
- Orders
- Quantity Sold
- Customers
- AOV
- Gross Profit
- Profit Margin
- Revenue Growth

### SQL Analysis

- Total revenue
- Total orders
- Total customers
- Total quantity
- Profit
- Margin
- Period comparisons

### Python Analysis

- KPI validation
- Descriptive statistics
- Trend analysis
- Performance profiling

### Power BI Output

Executive KPI cards and performance overview.

### Acceptance Criteria

All core KPIs must be calculated correctly and reconciled across analytical layers.

---

## REQ-002 — Revenue Trend

**Priority:** P0

### Business Question

How is ShopSphere's revenue changing over time?

### Required Data

- Order date
- Revenue
- Order status

### KPIs

- Net Revenue
- Revenue Growth
- MoM Growth
- YoY Growth
- Running Revenue

### SQL Analysis

- Daily revenue
- Monthly revenue
- Previous-period revenue
- Running totals

### Python Analysis

- Time-series aggregation
- Rolling averages
- Growth calculations

### Power BI Output

Revenue trend and growth visuals.

### Acceptance Criteria

Revenue trends must support daily, weekly, monthly, quarterly, and yearly analysis where data coverage permits.

---

## REQ-003 — Sales by Category

**Priority:** P0

### Business Question

Which product categories generate the most sales?

### Required Data

- Product
- Category
- Order items
- Revenue
- Quantity

### KPIs

- Category Revenue
- Category Orders
- Category Quantity
- Category Contribution

### SQL Analysis

Category-level aggregation and ranking.

### Python Analysis

Category comparison and contribution analysis.

### Power BI Output

Category performance charts.

### Acceptance Criteria

Category totals must reconcile with overall sales totals.

---

## REQ-004 — Sales Growth

**Priority:** P1

### Business Question

Which products and categories are growing or declining?

### Required Data

- Product
- Category
- Date
- Revenue

### KPIs

- Current Revenue
- Previous Revenue
- Growth %

### SQL Analysis

LAG-based period comparison.

### Python Analysis

Growth-rate analysis.

### Power BI Output

Growth ranking and trend visuals.

### Acceptance Criteria

Growth calculations must correctly handle periods with zero or missing prior-period revenue.

---

## REQ-005 — Customer Base

**Priority:** P0

### Business Question

How large and active is the ShopSphere customer base?

### Required Data

- Customer ID
- Order ID
- Order date
- Order status

### KPIs

- Total Customers
- Active Customers
- New Customers
- Returning Customers

### SQL Analysis

Distinct customer analysis.

### Python Analysis

Customer profiling.

### Power BI Output

Customer KPI cards.

### Acceptance Criteria

Customer counts must use distinct valid customer IDs.

---

## REQ-006 — New vs Returning Customers

**Priority:** P0

### Business Question

How much business comes from new versus returning customers?

### Required Data

- Customer ID
- Order ID
- Order date
- Revenue

### KPIs

- New Customers
- Returning Customers
- Repeat Purchase Rate
- Customer Revenue Contribution

### SQL Analysis

First-purchase identification and repeat-customer analysis.

### Python Analysis

Customer purchase-history analysis.

### Power BI Output

New vs returning customer visuals.

### Acceptance Criteria

Customer classification must be based on completed purchase history.

---

## REQ-007 — Customer Purchase Behavior

**Priority:** P1

### Business Question

How frequently and how much do customers purchase?

### Required Data

- Customer ID
- Order ID
- Order date
- Revenue

### KPIs

- Purchase Frequency
- Purchase Interval
- Monetary Value
- AOV

### SQL Analysis

Customer-level aggregations and purchase intervals.

### Python Analysis

Distribution and behavioral analysis.

### Power BI Output

Customer behavior analysis.

### Acceptance Criteria

Purchase frequency and interval calculations must be based on valid completed orders.

---

## REQ-008 — RFM Segmentation

**Priority:** P0

### Business Question

Which customers are most valuable and which customers are at risk?

### Required Data

- Customer ID
- Order date
- Revenue

### KPIs

- Recency
- Frequency
- Monetary
- RFM Score

### SQL Analysis

Customer-level purchase aggregation.

### Python Analysis

RFM scoring and segmentation.

### Power BI Output

RFM segment distribution and customer-value analysis.

### Acceptance Criteria

RFM methodology and scoring rules must be documented and reproducible.

---

## REQ-009 — Customer Retention

**Priority:** P0

### Business Question

Are customers returning to ShopSphere after their initial purchase?

### Required Data

- Customer ID
- Order date
- Revenue

### KPIs

- Repeat Purchase Rate
- Retention Rate
- Active Customers

### SQL Analysis

Repeat-purchase and cohort calculations.

### Python Analysis

Retention curves and lifecycle analysis.

### Power BI Output

Retention dashboard.

### Acceptance Criteria

Retention must be calculated using a clearly documented cohort methodology.

---

## REQ-010 — Cohort Analysis

**Priority:** P1

### Business Question

How does customer behavior change after their first purchase?

### Required Data

- Customer ID
- First purchase date
- Subsequent purchase dates

### KPIs

- Cohort Retention
- Active Customers
- Cohort Revenue

### SQL Analysis

Cohort creation using CTEs and date calculations.

### Python Analysis

Cohort retention matrix.

### Power BI Output

Cohort heatmap/matrix.

### Acceptance Criteria

Customers must be assigned to cohorts according to their first completed purchase.

---

## REQ-011 — Product Performance

**Priority:** P0

### Business Question

Which products perform best and worst?

### Required Data

- Product
- Category
- Quantity
- Revenue
- Profit
- Date

### KPIs

- Product Revenue
- Product Profit
- Product Margin
- Quantity
- Growth

### SQL Analysis

Product aggregation and ranking.

### Python Analysis

Product performance analysis.

### Power BI Output

Product performance dashboard.

### Acceptance Criteria

Product metrics must reconcile with category and total business metrics.

---

## REQ-012 — Product Profitability

**Priority:** P0

### Business Question

Which products generate high revenue but poor profitability?

### Required Data

- Product
- Revenue
- Product cost
- Discount
- Returns

### KPIs

- Revenue
- Profit
- Margin

### SQL Analysis

Revenue-profit ranking and segmentation.

### Python Analysis

Revenue vs profit analysis.

### Power BI Output

Revenue-profit matrix/scatter analysis.

### Acceptance Criteria

Profit must use the documented revenue and cost definitions.

---

## REQ-013 — Category Contribution

**Priority:** P1

### Business Question

How much does each category contribute to overall revenue and profit?

### Required Data

- Category
- Revenue
- Profit

### KPIs

- Category Contribution
- Category Profit
- Category Margin

### SQL Analysis

Category-level aggregation.

### Python Analysis

Contribution analysis.

### Power BI Output

Category contribution visuals.

### Acceptance Criteria

Category contributions must reconcile to overall totals.

---

## REQ-014 — Discount Performance

**Priority:** P0

### Business Question

How does discounting relate to revenue and profitability?

### Required Data

- Product
- Category
- Gross Sales
- Discount
- Revenue
- Profit

### KPIs

- Discount %
- Discount Amount
- Discount-to-Revenue
- Profit Margin

### SQL Analysis

Discount-band and product/category analysis.

### Python Analysis

Discount vs revenue/profit analysis.

### Power BI Output

Discount-performance dashboard.

### Acceptance Criteria

Analysis must distinguish association from causation.

---

## REQ-015 — Regional Performance

**Priority:** P1

### Business Question

Which geographic regions perform best?

### Required Data

- Country
- State
- City
- Region
- Revenue
- Profit
- Customers
- Orders

### KPIs

- Regional Revenue
- Regional Profit
- Regional Margin
- Regional AOV
- Customer Count
- Growth

### SQL Analysis

Geographic aggregation.

### Python Analysis

Regional comparisons.

### Power BI Output

Geographic performance map and ranking.

### Acceptance Criteria

Geographic totals must reconcile with company-level totals.

---

## REQ-016 — Delivery Performance

**Priority:** P1

### Business Question

How effectively are orders being delivered?

### Required Data

- Order date
- Ship date
- Delivery date
- Expected delivery date
- Region

### KPIs

- Order-to-Delivery Time
- Ship-to-Delivery Time
- Delayed Delivery Rate

### SQL Analysis

Delivery-time calculations.

### Python Analysis

Delivery distributions and regional comparisons.

### Power BI Output

Operations dashboard.

### Acceptance Criteria

Delivery metrics must exclude invalid date sequences.

---

## REQ-017 — Return Analysis

**Priority:** P1

### Business Question

Where are product returns concentrated?

### Required Data

- Order
- Product
- Category
- Customer
- Region
- Return quantity
- Return date

### KPIs

- Order Return Rate
- Item Return Rate
- Return Quantity

### SQL Analysis

Return analysis by product, category, customer, and geography.

### Python Analysis

Return-pattern analysis.

### Power BI Output

Returns dashboard.

### Acceptance Criteria

Order-level and item-level return rates must be calculated separately.

---

## REQ-018 — Statistical Analysis

**Priority:** P1

### Business Question

Which observed relationships or differences are statistically meaningful?

### Required Data

Relevant numerical and categorical analytical variables.

### Methods

- Descriptive statistics
- Correlation
- Covariance
- t-test
- ANOVA
- Chi-square
- Confidence intervals where appropriate

### Python Analysis

Statistical testing with documented assumptions.

### Power BI Output

Supporting statistical insights where useful.

### Acceptance Criteria

Every statistical test must have a business question, hypothesis, test rationale, assumptions, result, and business interpretation.

---

## REQ-019 — Time-Based Performance

**Priority:** P0

### Business Question

How does business performance change across different time periods?

### Required Data

- Order date
- Revenue
- Profit
- Orders
- Quantity

### KPIs

- Daily Performance
- Monthly Performance
- Quarterly Performance
- Yearly Performance
- MoM Growth
- YoY Growth
- Rolling Metrics
- Cumulative Metrics

### SQL Analysis

Date aggregation and window functions.

### Python Analysis

Resampling, shifting, rolling calculations.

### Power BI Output

Time-series dashboard.

### Acceptance Criteria

Time calculations must use a consistent date definition across SQL, Python, and Power BI.

---

## REQ-020 — Customer Value

**Priority:** P1

### Business Question

Which customers generate the greatest long-term value?

### Required Data

- Customer
- Revenue
- Orders
- Purchase dates
- Profit where available

### KPIs

- Historical Customer Value
- Estimated CLV

### SQL Analysis

Historical customer value.

### Python Analysis

CLV methodology and estimation.

### Power BI Output

Customer-value analysis.

### Acceptance Criteria

Historical customer value and estimated CLV must be clearly separated and assumptions documented.

---

# 4. Requirement Traceability Summary

| Requirement | Priority | Primary Analytical Layer | Power BI |
|---|---|---|---|
| REQ-001 | P0 | SQL + Python | Executive |
| REQ-002 | P0 | SQL + Python | Sales |
| REQ-003 | P0 | SQL + Python | Sales |
| REQ-004 | P1 | SQL + Python | Sales |
| REQ-005 | P0 | SQL + Python | Customer |
| REQ-006 | P0 | SQL + Python | Customer |
| REQ-007 | P1 | Python + SQL | Customer |
| REQ-008 | P0 | Python | Customer |
| REQ-009 | P0 | Python + SQL | Customer |
| REQ-010 | P1 | Python + SQL | Customer |
| REQ-011 | P0 | SQL + Python | Product |
| REQ-012 | P0 | SQL + Python | Product |
| REQ-013 | P1 | SQL + Python | Product |
| REQ-014 | P0 | SQL + Python | Product |
| REQ-015 | P1 | SQL + Python | Geography |
| REQ-016 | P1 | SQL + Python | Operations |
| REQ-017 | P1 | SQL + Python | Operations |
| REQ-018 | P1 | Python | Supporting |
| REQ-019 | P0 | SQL + Python | Sales |
| REQ-020 | P1 | Python + SQL | Customer |

---

# 5. Requirement Completion Rule

A requirement is considered complete only when:

1. Required data exists.
2. Data quality is validated.
3. KPI is calculated.
4. SQL implementation exists where applicable.
5. Python implementation exists where applicable.
6. Power BI implementation exists where applicable.
7. Results are validated.
8. Business interpretation is documented.

Therefore, a requirement cannot be marked complete merely because its documentation exists.