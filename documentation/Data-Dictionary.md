# Data Dictionary — Nexora Commerce

## Overview

This data dictionary describes the fields used in the Nexora Commerce — Retail Sales, Customer & Profitability Analytics project.

The project uses four related tables:

* Customers
* Products
* Orders
* Order Details

These tables were cleaned and transformed using Power Query before being loaded into Power BI.

---

# 1. Customers

The Customers table contains customer-level information used for customer segmentation and customer profitability analysis.

| Field             | Description                                                            | Data Type    |
| ----------------- | ---------------------------------------------------------------------- | ------------ |
| Customer_ID       | Unique identifier assigned to each customer.                           | Text / ID    |
| Customer_Name     | Name of the customer.                                                  | Text         |
| Gender            | Gender recorded for the customer.                                      | Text         |
| Age               | Age of the customer.                                                   | Whole Number |
| City              | City associated with the customer.                                     | Text         |
| State             | State associated with the customer in the original dataset.            | Text         |
| Region            | Geographic region associated with the customer.                        | Text         |
| Customer_Segment  | Customer classification such as Consumer, Corporate or Small Business. | Text         |
| Registration_Date | Date on which the customer registered.                                 | Date         |

### Data Preparation

* Missing `Customer_Segment` values were replaced with `Unknown`.
* Missing `City` values were replaced with `Unknown`.
* Text fields were trimmed to remove unnecessary spaces.
* `State` was removed from the cleaned Customers table because it was considered redundant for the final analysis.
* Duplicate `Customer_ID` values were checked.

---

# 2. Products

The Products table contains product-level information used for product, category and profitability analysis.

| Field         | Description                                                              | Data Type |
| ------------- | ------------------------------------------------------------------------ | --------- |
| Product_ID    | Unique identifier assigned to each product.                              | Text / ID |
| Product_Name  | Name of the product.                                                     | Text      |
| Category      | Main product category.                                                   | Text      |
| Subcategory   | More detailed classification within a product category.                  | Text      |
| Supplier      | Supplier associated with the product.                                    | Text      |
| Unit_Cost     | Cost associated with one unit of the product.                            | Decimal   |
| Selling_Price | Selling price of one unit before transaction-level discount adjustments. | Decimal   |

### Data Preparation

* Missing `Supplier` values were replaced with `Unknown`.
* Category text was standardized for consistent capitalization and formatting.
* Text fields were trimmed.
* Duplicate `Product_ID` values were checked.

---

# 3. Orders

The Orders table contains order-level information about customer purchases.

| Field          | Description                                                                | Data Type |
| -------------- | -------------------------------------------------------------------------- | --------- |
| Order_ID       | Unique identifier assigned to each order.                                  | Text / ID |
| Order_Date     | Date on which the order was placed.                                        | Date      |
| Customer_ID    | Identifier linking the order to the corresponding customer.                | Text / ID |
| Sales_Channel  | Channel through which the order was placed, such as Online or Store.       | Text      |
| Sales_Platform | Platform used for the sale, such as Website, Mobile App or Physical Store. | Text      |
| City           | City associated with the order.                                            | Text      |
| Region         | Geographic region associated with the order.                               | Text      |
| Payment_Method | Payment method used for the transaction.                                   | Text      |
| Order_Status   | Current status of the order.                                               | Text      |

### Data Preparation

* Duplicate Order IDs were checked.
* Blank Order IDs were checked.
* Text fields were reviewed for inconsistencies and trimmed where required.
* Date and other field data types were validated.

---

# 4. Order Details

The Order Details table contains product-level transaction information for each order.

This is the main transaction table used for sales, cost, profit, discount and quantity analysis.

| Field        | Description                                                                     | Data Type    |
| ------------ | ------------------------------------------------------------------------------- | ------------ |
| Order_ID     | Identifier linking the transaction detail to an order.                          | Text / ID    |
| Product_ID   | Identifier linking the transaction detail to a product.                         | Text / ID    |
| Quantity     | Number of units of the product included in the transaction.                     | Whole Number |
| Unit_Price   | Actual unit price used for the transaction.                                     | Decimal      |
| Discount     | Discount applied to the transaction, represented as a percentage/decimal value. | Decimal      |
| Sales_Amount | Total sales value generated by the transaction detail.                          | Decimal      |
| Cost_Amount  | Total cost associated with the transaction detail.                              | Decimal      |
| Profit       | Profit or loss generated by the transaction detail.                             | Decimal      |

### Data Preparation

* 8 records with `Quantity = 0` were removed.
* 20 exact duplicate rows were removed.
* Discount values, including the 50% discount records, were retained for analysis.
* Negative profit values were retained because they represent meaningful loss-making transactions.
* Financial fields were rounded to two decimal places.
* IDs and text values were trimmed.
* Data types were validated.

---

# 5. Relationships Between Tables

The four tables were connected in Power BI using the following relationships:

| From Table | From Field  | Relationship | To Table      | To Field    |
| ---------- | ----------- | ------------ | ------------- | ----------- |
| Customers  | Customer_ID | 1 → *        | Orders        | Customer_ID |
| Orders     | Order_ID    | 1 → *        | Order Details | Order_ID    |
| Products   | Product_ID  | 1 → *        | Order Details | Product_ID  |

### Relationship Structure

```text
Customers
    │
    │ Customer_ID
    ▼
Orders
    │
    │ Order_ID
    ▼
Order Details
    ▲
    │ Product_ID
    │
Products
```

The relationships allow customer, product and order information to be analyzed together in Power BI.

---

# 6. Key Analytical Fields

Several fields are particularly important for the project's business analysis.

| Analytical Area        | Important Fields                                                       |
| ---------------------- | ---------------------------------------------------------------------- |
| Sales Analysis         | Sales_Amount, Order_Date, Category, Subcategory, Region, Sales_Channel |
| Profitability Analysis | Sales_Amount, Cost_Amount, Profit, Unit_Price, Discount                |
| Customer Analysis      | Customer_ID, Customer_Name, Customer_Segment                           |
| Product Analysis       | Product_ID, Product_Name, Category, Subcategory                        |
| Regional Analysis      | Region, City                                                           |
| Channel Analysis       | Sales_Channel, Sales_Platform                                          |
| Discount Analysis      | Discount, Sales_Amount, Profit, Profit Margin %                        |

---

# 7. Data Model Purpose

The data model was designed to separate customer, product and order information from transaction-level details.

This structure allows the project to:

* Analyze sales across products and categories.
* Evaluate profitability at different levels.
* Compare customer segments.
* Analyze regional performance.
* Compare online and store channels.
* Investigate the relationship between discounts and profitability.
* Identify high-sales but loss-making products and customers.

---

## Note

The Nexora Commerce dataset is a synthetic dataset created for portfolio and learning purposes. It is not based on actual company transactions.
