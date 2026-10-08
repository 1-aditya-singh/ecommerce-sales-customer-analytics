# ShopSphere KPI Dictionary

## 1. Purpose

This document defines the official Key Performance Indicators (KPIs) used throughout the ShopSphere E-Commerce Sales & Customer Analytics System.

A KPI is a measurable indicator used to evaluate business performance.

The KPI dictionary provides a single definition for each metric so that SQL, Python, and Power BI do not calculate the same business concept differently.

---

# 2. KPI Calculation Principles

All KPIs must have:

- Clear business definition
- Explicit formula
- Defined grain
- Required source fields
- Defined business meaning
- Validation rule
- Consistent treatment of order status
- Consistent treatment of discounts
- Consistent treatment of returns
- Consistent treatment of cancellations

---

# 3. Financial KPI Backbone

The primary financial flow is:

Gross Sales
→ Discount Amount
→ Returned Sales
→ Cancelled Sales
→ Net Revenue
→ COGS
→ Gross Profit
→ Profit Margin

---

# 4. Sales KPIs

## KPI-001 — Gross Sales

**Definition:** Total sales value before discounts, returns, and cancellations.

**Formula:**

Gross Sales = SUM(Unit Price × Quantity)

**Grain:** Order-item

**Business Meaning:** Measures total merchandise sales before deductions.

**Validation:** Reconcile order-item aggregation with SQL and Python.

---

## KPI-002 — Discount Amount

**Definition:** Total monetary value of discounts applied to sales.

**Formula:**

Discount Amount = SUM(Discount Amount)

or, where applicable:

Gross Sales × Discount %

**Grain:** Order-item

**Business Meaning:** Measures revenue reduction attributable to discounts.

**Validation:** Discount amount must not exceed applicable gross sales.

---

## KPI-003 — Net Revenue

**Definition:** Revenue remaining after defined discounts, returns, and cancellations.

**Formula:**

Net Revenue =
Gross Sales
− Discount Amount
− Returned Sales
− Cancelled Sales

**Grain:** Order / Order-item depending on implementation.

**Business Meaning:** Primary sales KPI for financial performance analysis.

**Validation:** Must reconcile across Python, SQL, and Power BI.

---

## KPI-004 — Orders

**Definition:** Number of distinct valid completed orders.

**Formula:**

COUNT(DISTINCT Order ID)

subject to documented order-status rules.

**Grain:** Order

**Business Meaning:** Measures transaction volume.

**Validation:** No duplicate valid order IDs.

---

## KPI-005 — Quantity Sold

**Definition:** Total quantity of products sold through valid orders.

**Formula:**

SUM(Quantity)

**Grain:** Order-item

**Business Meaning:** Measures unit volume.

---

## KPI-006 — Average Order Value (AOV)

**Definition:** Average net revenue generated per completed order.

**Formula:**

AOV = Net Revenue / Completed Orders

**Grain:** Order

**Business Meaning:** Measures average customer order value.

**Important:** AOV is not the same as average product selling price.

---

## KPI-007 — Average Selling Price (ASP)

**Definition:** Average net product revenue generated per unit sold.

**Formula:**

ASP = Net Product Revenue / Quantity Sold

**Grain:** Order-item

**Business Meaning:** Measures average realized selling price per unit.

---

## KPI-008 — Gross Profit

**Definition:** Revenue remaining after product cost.

**Formula:**

Gross Profit = Net Revenue − COGS

**Grain:** Order-item / product transaction

**Business Meaning:** Measures profitability before operating expenses.

---

## KPI-009 — Profit Margin

**Definition:** Percentage of net revenue retained as gross profit.

**Formula:**

Profit Margin = Gross Profit / Net Revenue × 100

**Business Meaning:** Measures profitability efficiency.

**Validation:** Handle zero-revenue periods safely.

---

## KPI-010 — Revenue Growth

**Definition:** Percentage change in revenue between comparable periods.

**Formula:**

(Current Revenue − Previous Revenue)
/
Previous Revenue × 100

**Business Meaning:** Measures sales growth or decline.

---

# 5. Customer KPIs

## KPI-011 — Total Customers

**Definition:** Number of distinct customers in the customer master.

**Formula:**

COUNT(DISTINCT Customer ID)

**Grain:** Customer

---

## KPI-012 — Active Customers

**Definition:** Customers with at least one valid completed purchase during the selected period.

**Grain:** Customer-period

---

## KPI-013 — New Customers

**Definition:** Customers whose first completed purchase occurs during the selected period.

**Grain:** Customer-period

---

## KPI-014 — Returning Customers

**Definition:** Customers who purchase during the selected period and had a completed purchase before that period.

**Grain:** Customer-period

---

## KPI-015 — Repeat Purchase Rate

**Definition:** Percentage of customers with at least two completed purchases within the defined analysis window.

**Formula:**

Repeat Customers / Purchasing Customers × 100

**Business Meaning:** Measures repeat purchasing behavior.

---

## KPI-016 — Purchase Frequency

**Definition:** Average number of completed orders per active customer.

**Formula:**

Completed Orders / Active Customers

---

## KPI-017 — Purchase Interval

**Definition:** Average number of days between consecutive completed purchases for repeat customers.

**Business Meaning:** Measures purchase-cycle behavior.

---

## KPI-018 — Customer Revenue Contribution

**Definition:** Percentage of total net revenue generated by a customer or customer segment.

**Formula:**

Customer Net Revenue / Total Net Revenue × 100

---

## KPI-019 — Customer Profit Contribution

**Definition:** Percentage of total profit generated by a customer or customer segment.

**Formula:**

Customer Profit / Total Profit × 100

---

## KPI-020 — Historical Customer Value

**Definition:** Total actual net revenue generated by a customer over the observed historical period.

**Formula:**

SUM(Customer Net Revenue)

**Important:** This is historical value, not a forecast.

---

# 6. RFM KPIs

## KPI-021 — Recency

**Definition:** Number of days since the customer's most recent completed purchase.

**Formula:**

Analysis Date − Last Purchase Date

**Business Meaning:** Measures how recently a customer purchased.

---

## KPI-022 — Frequency

**Definition:** Number of completed purchases made by a customer during the analysis period.

---

## KPI-023 — Monetary

**Definition:** Total net revenue generated by a customer during the analysis period.

---

## KPI-024 — RFM Score

**Definition:** Composite customer score based on Recency, Frequency, and Monetary values.

**Business Meaning:** Supports customer segmentation and prioritization.

**Important:** Scoring methodology must be data-driven and documented.

---

# 7. Retention KPIs

## KPI-025 — Retention Rate

**Definition:** Percentage of customers from an original cohort who remain active in a later period.

**Formula:**

Retained Cohort Customers
/
Original Cohort Customers × 100

---

## KPI-026 — Cohort Retention

**Definition:** Retention percentage calculated for each customer acquisition/first-purchase cohort and subsequent period.

**Business Meaning:** Measures customer lifecycle performance.

---

# 8. Product KPIs

## KPI-027 — Product Revenue

**Definition:** Net revenue generated by a product.

---

## KPI-028 — Product Profit

**Definition:** Gross profit generated by a product.

---

## KPI-029 — Product Margin

**Definition:** Profitability percentage of a product.

**Formula:**

Product Profit / Product Revenue × 100

---

## KPI-030 — Category Contribution

**Definition:** Percentage of total revenue generated by a product category.

**Formula:**

Category Revenue / Total Revenue × 100

---

# 9. Discount KPIs

## KPI-031 — Discount Percentage

**Definition:** Percentage of gross sales represented by discounts.

**Formula:**

Discount Amount / Gross Sales × 100

---

## KPI-032 — Discount Amount

**Definition:** Total monetary discount provided.

**Note:** KPI-002 and KPI-032 represent the same business metric at different dictionary sections and must use one consistent implementation.

---

## KPI-033 — Discount-to-Revenue

**Definition:** Discount amount relative to net revenue.

**Formula:**

Discount Amount / Net Revenue × 100

**Business Meaning:** Measures discount intensity relative to realized revenue.

---

# 10. Geographic KPIs

## KPI-034 — Regional Revenue

**Definition:** Net revenue generated within a geographic region.

---

## KPI-035 — Regional Profit

**Definition:** Gross profit generated within a geographic region.

---

## KPI-036 — Regional AOV

**Definition:** Average order value for a geographic region.

**Formula:**

Regional Net Revenue / Regional Completed Orders

---

# 11. Operations KPIs

## KPI-037 — Order Return Rate

**Definition:** Percentage of completed orders associated with a return.

**Formula:**

Returned Orders / Completed Orders × 100

---

## KPI-038 — Item Return Rate

**Definition:** Percentage of sold units that are returned.

**Formula:**

Returned Quantity / Sold Quantity × 100

---

## KPI-039 — Return Quantity

**Definition:** Total number of units returned.

**Formula:**

SUM(Return Quantity)

---

## KPI-040 — Order-to-Delivery Time

**Definition:** Number of days between order placement and delivery.

**Formula:**

Delivery Date − Order Date

---

## KPI-041 — Ship-to-Delivery Time

**Definition:** Number of days between shipment and delivery.

**Formula:**

Delivery Date − Ship Date

---

## KPI-042 — Delayed Delivery Rate

**Definition:** Percentage of delivered orders delivered after the expected delivery date.

**Formula:**

Delayed Orders / Delivered Orders × 100

**Business Meaning:** Measures delivery service performance.

---

## KPI-043 — Cancellation Rate

**Definition:** Percentage of orders cancelled.

**Formula:**

Cancelled Orders / Total Orders × 100

---

# 12. KPI Implementation Standard

Every KPI must eventually exist consistently across the analytical system where applicable:

| Layer | Responsibility |
|---|---|
| PostgreSQL | Store source data |
| SQL | Analytical calculation |
| Python | Independent analytical calculation/validation |
| Power BI | Business presentation |
| DAX | Semantic-layer calculation |
| Validation | Cross-system reconciliation |

---

# 13. KPI Validation Principles

For important KPIs, the following must reconcile:

Python KPI
=
SQL KPI
=
Power BI KPI

Important reconciliation metrics:

- Revenue
- Orders
- Customers
- Quantity
- Profit
- AOV
- Margin

Any discrepancy must be investigated before the project is considered complete.

---

# 14. KPI Governance Rules

1. KPI definitions must not change silently.
2. KPI formulas must be documented.
3. Order-status treatment must be consistent.
4. Return treatment must be consistent.
5. Cancellation treatment must be consistent.
6. Duplicate transactions must not inflate KPIs.
7. Null and invalid values must be handled according to documented rules.
8. Division-by-zero conditions must be handled.
9. KPI grain must be clearly defined.
10. SQL, Python, and Power BI must use consistent business definitions.