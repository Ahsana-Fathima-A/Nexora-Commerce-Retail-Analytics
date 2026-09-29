# DAX Measures — Nexora Commerce

## Overview

This document contains the main DAX measures used in the Nexora Commerce — Retail Sales, Customer & Profitability Analytics project.

The measures were created in Power BI to calculate key business performance indicators used across the dashboard.

---

## 1. Total Sales

```DAX
Total Sales =
SUM(order_details_clean[Sales_Amount])
```

**Purpose:** Calculates the total sales/revenue generated from all valid order-detail records.

**Format:** Currency (₹)

---

## 2. Total Cost

```DAX
Total Cost =
SUM(order_details_clean[Cost_Amount])
```

**Purpose:** Calculates the total cost associated with the analyzed transactions.

**Format:** Currency (₹)

---

## 3. Total Profit

```DAX
Total Profit =
SUM(order_details_clean[Profit])
```

**Purpose:** Calculates total profit or loss by summing transaction-level profit.

**Format:** Currency (₹)

---

## 4. Profit Margin %

```DAX
Profit Margin % =
DIVIDE(
    [Total Profit],
    [Total Sales],
    0
)
```

**Purpose:** Measures profitability relative to total sales.

**Format:** Percentage

**Interpretation:** A negative value indicates that the analyzed sales generated a loss rather than a profit.

---

## 5. Total Order

```DAX
Total Order =
DISTINCTCOUNT(orders_clean[Order_ID])
```

**Purpose:** Calculates the number of unique orders using the Order ID.

**Format:** Whole number

---

## 6. Total Customers

```DAX
Total Customers =
DISTINCTCOUNT(orders_clean[Customer_ID])
```

**Purpose:** Calculates the number of unique customers associated with the orders.

**Format:** Whole number

---

## 7. Total Quantity

```DAX
Total Quantity =
SUM(order_details_clean[Quantity])
```

**Purpose:** Calculates the total quantity of products sold across valid order-detail records.

**Format:** Whole number

---

## 8. Average Order Value

```DAX
Average Order Value =
DIVIDE(
    [Total Sales],
    [Total Order],
    0
)
```

**Purpose:** Calculates the average sales value generated per unique order.

**Format:** Currency (₹)

---

## Measure Summary

| Measure             | Business Purpose                              |
| ------------------- | --------------------------------------------- |
| Total Sales         | Measures overall sales/revenue                |
| Total Cost          | Measures total transaction cost               |
| Total Profit        | Measures overall profit or loss               |
| Profit Margin %     | Measures profitability relative to sales      |
| Total Order         | Counts unique orders                          |
| Total Customers     | Counts unique customers                       |
| Total Quantity      | Measures total units sold                     |
| Average Order Value | Measures average sales value per unique order |

---

## How the Measures Were Used

These measures were used throughout the Power BI dashboard to analyze:

* Sales performance
* Profitability
* Product and category performance
* Regional performance
* Customer segments
* Customer profitability
* Sales channels
* Discount levels
* High-sales and loss-making products

The measures were designed to support the project's business questions rather than simply provide additional KPIs.

---

## Key Analytical Principle

The project evaluates **profitability alongside sales**.

High sales do not necessarily indicate strong business performance. The dashboard therefore compares sales, cost, profit and profit margin to identify areas where revenue is being generated without sufficient profitability.
