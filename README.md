# 🍕 MySQL's Project: Pizza Sales Analysis

Proyek ini menampilkan analisis data penjualan menggunakan SQL untuk mengidentifikasi tren penjualan, kinerja produk, dan metrik bisnis utama pada sebuah toko pizza.
---

## Objectives

- Analyze revenue and sales trends.
- Identify top-performing and underperforming pizzas.
- Extract key performance indicators (KPIs).
- Support data-driven business recommendations. 

---

## Dataset Description

- Rows: 48,620
- Period: Full year 2015
- Fields: `pizza_id`, `order_id`, `pizza_name_id`, `quantity`, `order_date`, `order_time`, `unit_price`, `total_price`, `pizza_category`, `pizza_size`, `pizza_ingredients`, `pizza_name`

---

## Tools & Technologies

- MySQL Workbench 80
- Excel (optional for data cleaning)

---

## 📈 A. Key Performance Indicators (KPIs)

### 1. Total Revenue

```sql
SELECT SUM(total_price) AS Total_Revenue
FROM project_pizzasales;
```

### 2. Average Order Value
```sql 
SELECT (SUM(total_price) / COUNT(DISTINC order_id)) AS Avg_Order_Value
FROM project_pizzasales;
