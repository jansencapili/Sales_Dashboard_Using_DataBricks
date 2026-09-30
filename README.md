# Sales Performance Dashboard — Built with Databricks

A comprehensive **AI/BI Dashboard** built in Databricks that provides a full overview of sales metrics, revenue trends, and performance analysis across products and regions. An interactive date filter lets you drill into specific time periods.

![Sales Performance Dashboard](Sales%20Performance%20Dashboard.jpg)

---

## Dashboard Preview

![Sales Performance Dashboard](Sales%20Performance%20Dashboard.jpg)

> **Note:** The screenshot image (`Sales Performance Dashboard.jpg`) must be placed in the root of this repository for the preview to render. Export it from the Databricks dashboard view and commit it alongside this README.

---

## Key Metrics at a Glance

| Metric | Value |
| --- | --- |
| Total Orders | 27,659 |
| Total Customers | 18,484 |
| Total Revenue | $29,356,250 |

---

## Dashboard Widgets & Visualizations

The dashboard is organized into a single page — **Sales Dashboard** — containing the following widgets:

| Widget | Type | Description |
| --- | --- | --- |
| **Total Orders** | Counter | Distinct count of order numbers across all sales records |
| **Total Customers** | Counter | Total number of unique customers |
| **Total Revenue** | Counter | Sum of all sales amounts |
| **Revenue Trend Over Time** | Line Chart | Revenue aggregated by year, showing the trend from 2010 to 2014 |
| **Revenue by Category** | Bar Chart | Revenue breakdown by product category (Bikes, Accessories, Clothing) |
| **Revenue by Country** | Bar Chart | Revenue distribution across customer countries |
| **Year** | Date Range Filter | Interactive filter to narrow the analysis to a specific date range |

---

## Revenue Trend Over Time (2010–2014)

| Year | Revenue |
| --- | --- |
| 2010 | $43,419 |
| 2011 | $7,075,088 |
| 2012 | $5,842,231 |
| 2013 | $16,344,878 |
| 2014 | $45,642 |

Revenue peaked in **2013** at over $16.3M, with 2011 and 2012 also showing strong performance. The data spans five years of sales activity.

---

## Revenue by Product Category

| Category | Revenue | Share |
| --- | --- | --- |
| Bikes | $28,316,272 | 96.5% |
| Accessories | $700,262 | 2.4% |
| Clothing | $339,716 | 1.2% |

**Bikes** dominate the product mix, accounting for over 96% of total revenue.

---

## Revenue by Country

| Country | Revenue |
| --- | --- |
| United States | $9,162,327 |
| Australia | $9,060,172 |
| United Kingdom | $3,391,376 |
| Germany | $2,894,066 |
| France | $2,643,751 |
| Canada | $1,977,738 |

The **United States** and **Australia** are the top-performing markets, each generating over $9M in revenue. Together they account for roughly 62% of total sales.

---

## Underlying Data Model

The dashboard is powered by three datasets organized in a classic star schema:

### `fact_sales` (Fact Table)

| Column | Type | Description |
| --- | --- | --- |
| `order_number` | string | Unique order identifier |
| `product_key` | integer | Foreign key to `dim_products` |
| `customer_key` | integer | Foreign key to `dim_customers` |
| `order_date` | date | Date the order was placed |
| `shipping_date` | date | Date the order was shipped |
| `due_date` | date | Date the order is due |
| `sales_amount` | integer | Total sales amount for the line item |
| `quantity` | integer | Quantity ordered |
| `price` | integer | Unit price |
| `count` | integer | Row count |

### `dim_products` (Product Dimension)

| Column | Type | Description |
| --- | --- | --- |
| `product_key` | integer | Primary key (joins to `fact_sales.product_key`) |
| `product_id` | integer | Source product ID |
| `product_number` | string | Product number / SKU |
| `product_name` | string | Product name |
| `category_id` | string | Category identifier |
| `category` | string | Product category (Bikes, Accessories, Clothing) |
| `subcategory` | string | Product subcategory |
| `maintenance` | string | Maintenance requirement |
| `cost` | integer | Product cost |
| `product_line` | string | Product line |
| `start_date` | date | Product start date |
| `count` | integer | Row count |

### `dim_customers` (Customer Dimension)

| Column | Type | Description |
| --- | --- | --- |
| `customer_key` | integer | Primary key (joins to `fact_sales.customer_key`) |
| `customer_id` | integer | Source customer ID |
| `customer_number` | string | Customer number |
| `first_name` | string | Customer first name |
| `last_name` | string | Customer last name |
| `country` | string | Customer country |
| `marital_status` | string | Marital status |
| `gender` | string | Gender |
| `birthdate` | date | Customer birth date |
| `create_date` | date | Customer account creation date |
| `count` | integer | Row count |

---

## Data Relationships

```
dim_products ──── product_key ──┐
                               ├──> fact_sales
dim_customers ──── customer_key┘
```

- `fact_sales.product_key` → `dim_products.product_key` (many-to-one)
- `fact_sales.customer_key` → `dim_customers.customer_key` (many-to-one)

This star schema enables efficient aggregation across product categories and customer geographies while keeping the fact table lean for fast metric computation.

---

## How to Use

1. Open the dashboard in Databricks AI/BI Dashboards.
2. Use the **Year** date range filter at the top to focus on a specific period.
3. Review the KPI counters (Total Orders, Total Customers, Total Revenue) for a quick summary.
4. Explore the **Revenue Trend Over Time** line chart for year-over-year growth patterns.
5. Drill into **Revenue by Category** and **Revenue by Country** for product and regional breakdowns.

---

## Tech Stack

* **Databricks AI/BI Dashboards** — dashboard authoring and visualization
* **Databricks SQL Warehouse** — query execution
* **Unity Catalog** — data governance and storage

---

## Repository Contents

| File | Description |
| --- | --- |
| `README.md` | This file — project overview and documentation |
| `Sales Performance Dashboard.lvdash.json` | The Databricks AI/BI Dashboard definition file |
| `Sales Performance Dashboard.jpg` | Screenshot of the dashboard (to be added) |

