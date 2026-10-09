# DAX Measures | Superstore Sales Analysis

This document contains the key DAX measures used in the Power BI dashboard.

## 1. Sales and Profit Measures

### Total Sales

```dax
Total Sales = SUM(Orders[Sales])
```

### Total Profit

```dax
Total Profit = SUM(Orders[Profit])
```

### Total Quantity

```dax
Total Quantity = SUM(Orders[Quantity])
```

## 2. Order and Customer Measures

### Total Orders

```dax
Total Orders = DISTINCTCOUNT(Orders[Order ID])
```

### Total Customers

```dax
Total Customers = DISTINCTCOUNT(Orders[Customer ID])
```

### Average Order Value

```dax
Average Order Value = DIVIDE([Total Sales], [Total Orders])
```

### Orders per Customer

```dax
Orders per Customer = DIVIDE([Total Orders], [Total Customers])
```

## 3. Profitability Measures

### Profit Margin %

```dax
Profit Margin % = DIVIDE([Total Profit], [Total Sales])
```

### Average Discount %

```dax
Avg Discount % = AVERAGE(Orders[Discount])
```

## 4. Year-over-Year Analysis

### Sales Last Year

```dax
Sales LY =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR(DimDate[Date])
)
```

### Sales YoY %

```dax
Sales YoY % =
DIVIDE([Total Sales] - [Sales LY], [Sales LY])
```

### Profit Last Year

```dax
Profit LY =
CALCULATE(
    [Total Profit],
    SAMEPERIODLASTYEAR(DimDate[Date])
)
```

### Profit YoY %

```dax
Profit YoY % =
DIVIDE([Total Profit] - [Profit LY], [Profit LY])
```

## 5. Shipping Analysis

### Average Shipping Days

```dax
Avg Ship Days =
AVERAGEX(
    Orders,
    DATEDIFF(Orders[Order Date], Orders[Ship Date], DAY)
)
```

## 6. Loss Analysis

### Loss Orders

```dax
Loss Orders =
CALCULATE(
    DISTINCTCOUNT(Orders[Order ID]),
    Orders[Profit] < 0
)
```

### Loss Order %

```dax
Loss Order % = DIVIDE([Loss Orders], [Total Orders])

