# DAX Measures & Calculated Objects

This document contains all DAX measures, calculated tables, Power Query code, and calculated columns used in the **Brazilian E-Commerce (Olist) Power BI Dashboard**.

---

# Measures Table

## Revenue Measures

### Total Product Revenue

```DAX
Total Product Revenue =
SUM(order_items[price])
```

### Total Freight Revenue

```DAX
Total Freight Revenue =
SUM(order_items[freight_value])
```

### Total Revenue

```DAX
Total Revenue =
[Total Product Revenue] + [Total Freight Revenue]
```

### Revenue Per Customer

```DAX
Revenue Per Customer =
DIVIDE(
    [Total Revenue],
    [Total Customers]
)
```

### Revenue Prior Month

```DAX
Revenue Prior Month =
CALCULATE(
    [Total Revenue],
    DATEADD(Dim_Date[Date], -1, MONTH)
)
```

### Revenue MoM %

```DAX
Revenue MoM % =
DIVIDE(
    [Total Revenue] - [Revenue Prior Month],
    [Revenue Prior Month]
)
```

---

# Customer Measures

### Total Customers

```DAX
Total Customers =
DISTINCTCOUNT(customers[customer_unique_id])
```

### Distinct Customers

```DAX
Distinct Customers =
DISTINCTCOUNT(customers[customer_unique_id])
```

### Customer Frequency

```DAX
Customer Frequency =
DISTINCTCOUNT(orders[order_id])
```

### Customer Monetary Value

```DAX
Customer Monetary Value =
[Total Revenue]
```

### Repeat Customers

```DAX
Repeat Customers =
CALCULATE(
    DISTINCTCOUNT(customers[customer_unique_id]),
    FILTER(
        VALUES(customers[customer_unique_id]),
        CALCULATE(DISTINCTCOUNT(orders[order_id])) > 1
    )
)
```

### Repeat Purchase Rate %

```DAX
Repeat Purchase Rate % =
DIVIDE([Repeat Customers],[Distinct Customers])
```

---

# Order Measures

### Total Orders

```DAX
Total Orders =
DISTINCTCOUNT(orders[order_id])
```

### Total Items Sold

```DAX
Total Items Sold =
COUNTROWS(order_items)
```

### Average Order Value

```DAX
Average Order Value =
DIVIDE(
    [Total Revenue],
    [Total Orders]
)
```

---

# Delivery Measures

### Average Delivery Days

```DAX
Average Delivery Days =
AVERAGEX(
    orders,
    DATEDIFF(
        orders[order_purchase_timestamp],
        orders[order_delivered_customer_date],
        DAY
    )
)
```

### Average Delivery Time (Days)

```DAX
Average Delivery Time (Days) =
AVERAGEX(
    orders,
    DATEDIFF(
        orders[order_purchase_timestamp],
        orders[order_delivered_customer_date],
        DAY
    )
)
```

### Delivery Delay Days

```DAX
Delivery Delay Days =
AVERAGEX(
    orders,
    DATEDIFF(
        orders[order_estimated_delivery_date],
        orders[order_delivered_customer_date],
        DAY
    )
)
```

### On-Time Orders

```DAX
On-Time Orders =
CALCULATE(
    [Total Orders],
    FILTER(
        orders,
        orders[order_delivered_customer_date]
            <= orders[order_estimated_delivery_date]
    )
)
```

### On-Time %

```DAX
On-Time % =
DIVIDE(
    [On-Time Orders],
    [Total Orders]
)
```

### % Orders Late

```DAX
% Orders Late =
DIVIDE(
    CALCULATE(
        COUNTROWS(orders),
        orders[Delivery Status] = "Late"
    ),
    COUNTROWS(orders)
)
```

---

# Review Measures

### Average Review Score

```DAX
Average Review Score =
AVERAGE(order_reviews[review_score])
```

### Avg Review Score (On Time)

```DAX
Avg Review Score (On Time) =
CALCULATE(
    [Average Review Score],
    orders[Delivery Status] = "On Time"
)
```

### Avg Review Score (Late)

```DAX
Avg Review Score (Late) =
CALCULATE(
    [Average Review Score],
    orders[Delivery Status] = "Late"
)
```

---

# Calculated Tables

## RFM Table

```DAX
RFM_Table =
ADDCOLUMNS(
    SUMMARIZE(
        orders,
        customers[customer_unique_id]
    ),
    "Frequency", CALCULATE(DISTINCTCOUNT(orders[order_id])),
    "Monetary", CALCULATE([Total Revenue]),
    "RecencyDays",
        CALCULATE(
            DATEDIFF(
                MAX(orders[order_purchase_timestamp]),
                CALCULATE(MAX(orders[order_purchase_timestamp]),ALL(orders)),
                DAY
            )
        )
)
```

---

# Date Table (Power Query)

```PowerQuery
StartDate = #date(2016,1,1)
EndDate   = #date(2018,12,31)
```

Creates:

- Date
- Year
- Month Number
- Month Name
- Quarter
- YearMonth

---

# Calculated Columns

## Customer State Name

Converts Brazilian state abbreviations into full state names.

Example:

- SP → São Paulo
- RJ → Rio de Janeiro
- MG → Minas Gerais

---

## Order Date Only

```DAX
Order Date Only =
DATEVALUE(orders[order_purchase_timestamp])
```
