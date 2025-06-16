# 🍕 MySQL's Project: Pizza Sales Analysis

Proyek ini menampilkan analisis data penjualan menggunakan SQL untuk mengidentifikasi tren penjualan, kinerja produk, dan metrik bisnis utama pada sebuah toko pizza.
---

## Objectives

- Menganalisis tren pendapatan dan penjualan.
- Mengidentifikasi pizza dengan kinerja terbaik dan yang berkinerja buruk.
- Mengekstrak indikator kinerja utama (KPI).
- Mendukung rekomendasi bisnis berdasarkan data.

---

## Dataset Description

- Baris: 48,620
- Periode: Sepanjang tahun 2015
- Bidang: `pizza_id`, `order_id`, `pizza_name_id`, `quantity`, `order_date`, `order_time`, `unit_price`, `total_price`, `pizza_category`, `pizza_size`, `pizza_ingredients`, `pizza_name`

---

## Tools & Technologies

- MySQL Workbench 80
- Excel (optional for data cleaning)

---

## 📈 A. Key Performance Indicators (KPIs)

### 1. Total Revenue

### Input
```sql
SELECT SUM(total_price) AS Total_Revenue
FROM project_pizzasales;
```
### Output 
| Total_Revenue | 
|---------------|        
| 1087861.11    | 


### 2. Average Order Value

### Input
```sql 
SELECT (SUM(total_price) / COUNT(DISTINC order_id)) AS Avg_Order_Value
FROM project_pizzasales;
```
### Output 
| Avg_Order_Value | 
|---------------|        
| 38.307262    |
