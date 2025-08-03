# 🛒 Zepto E-commerce SQL Data Analysis Project

A complete PostgreSQL-based SQL project using a real-world e-commerce inventory dataset from **Zepto**, one of India’s fastest-growing quick-commerce startups. This project demonstrates end-to-end data analytics skills — from data exploration to business-focused insights — using real analyst techniques like **CASE**, **JOINS**, **CTEs**, and **Subqueries**.

---

## 📌 Project Highlights

- ✅ Realistic SQL project with retail use-case
- 🧹 Data cleaning & transformation (e.g. paise → rupees)
- 📊 Business insights: revenue, stock status, product value
- 🧠 Uses advanced SQL techniques: `CASE`, `JOIN`, `CTEs`, `Subqueries`
- 💼 Perfect for interview prep, portfolio building, or SQL learning

---

## 📁 Dataset Summary

- Source: Kaggle (scraped from Zepto’s mobile app)
- Real-world e-commerce catalog structure
- Duplicate product names with different packaging/weights
- Each row = unique SKU (Stock Keeping Unit)

### 🔧 Columns

| Column | Description |
|--------|-------------|
| sku_id | Unique product ID |
| name | Product name |
| category | Product category (e.g. Fruits, Snacks) |
| mrp | Max Retail Price (₹) |
| discountPercent | % discount on MRP |
| discountedSellingPrice | Final discounted price |
| availableQuantity | Inventory units available |
| weightInGms | Product weight (grams) |
| outOfStock | Boolean - Is the product out of stock? |
| quantity | No. of units per SKU |

---

## 🚀 SQL Features Demonstrated

### 🧹 Data Cleaning
- Removed products with MRP or price = 0
- Converted `mrp` & `discountedSellingPrice` from paise to rupees
- Handled null values and inconsistent entries

### 🔍 Data Exploration
- Counted total rows
- Identified distinct categories
- Compared stock vs out-of-stock
- Detected repeated product names (same product, different SKU)

### 📊 Business Queries
- Top discounted products
- High MRP but out-of-stock products
- Revenue by category
- Expensive products with low discount
- Avg. discount by category
- Price-per-gram value ranking

---

## ✅ 1. Top 10 products with highest discount %
```sql
SELECT DISTINCT name, mrp, discountPercent
FROM zepto
ORDER BY discountPercent DESC
LIMIT 10;
```

## 📸 Output Screenshots 

<img width="675" height="459" alt="Screenshot 2025-08-04 012115" src="https://github.com/user-attachments/assets/0b93bc71-2f7e-4d36-b702-13abe7a697fa" />

---


## ✅ 2. High-MRP products that are out of stock

```sql
SELECT DISTINCT name, mrp 
FROM zepto
WHERE outOfStock = TRUE AND mrp > 300
ORDER BY mrp DESC;
```

## 📸 Output Screenshots 

<img width="630" height="278" alt="Screenshot 2025-08-04 012138" src="https://github.com/user-attachments/assets/27606ed7-1987-4023-8482-b98569f209b7" />

---


## ✅ 3. Estimated revenue per category
```sql
SELECT category,
SUM(discountedSellingPrice * availableQuantity) AS total_revenue
FROM zepto
GROUP BY category
ORDER BY total_revenue DESC;
```
## 📸 Output Screenshots

<img width="400" height="583" alt="Screenshot 2025-08-04 012202" src="https://github.com/user-attachments/assets/5c258dae-1891-44e9-a927-8745d731c292" />

---




## ✅ 4. Expensive products (MRP > ₹500) with low discount (< 10%)

```sql
SELECT DISTINCT name, mrp, discountPercent
FROM zepto
WHERE mrp > 500 AND discountPercent < 10
ORDER BY mrp DESC, discountPercent DESC;
```

## 📸 Output Screenshots

<img width="895" height="551" alt="Screenshot 2025-08-04 012222" src="https://github.com/user-attachments/assets/d630dfa9-9cd1-4735-a23a-0b23c0584ce8" />

---


## ✅ 5. Top 5 categories with highest average discount %

```sql
SELECT category,
ROUND(AVG(discountPercent), 2) AS avg_discount
FROM zepto
GROUP BY category 
ORDER BY avg_discount DESC
LIMIT 5;
```

## 📸 Output Screenshots

<img width="384" height="300" alt="Screenshot 2025-08-04 012239" src="https://github.com/user-attachments/assets/ee7a9ea0-2049-47d6-b173-faa96c2f1dfd" />

---



## ✅ 6. Price per gram (value for money)
```sql
SELECT DISTINCT name, weightInGms, discountedSellingPrice,
ROUND(discountedSellingPrice / weightInGms, 2) AS price_per_gram
FROM zepto
WHERE weightInGms >= 100
ORDER BY price_per_gram;
```
## 📸 Output Screenshots

<img width="1100" height="535" alt="Screenshot 2025-08-04 012255" src="https://github.com/user-attachments/assets/1c2eae94-c571-4cb3-aca7-ed1e96dbe151" />

---



 ## ✅ 7. Classify product by weight (CASE statement)
 
```sql
SELECT DISTINCT name, weightInGms,
  CASE 
    WHEN weightInGms < 1000 THEN 'Low'
    WHEN weightInGms > 5000 THEN 'Medium'
    ELSE 'Bulk'
  END AS weight_category
FROM zepto;
```
## 📸 Output Screenshots

<img width="1018" height="561" alt="Screenshot 2025-08-04 012313" src="https://github.com/user-attachments/assets/24747a21-16f7-47cd-9f6e-17a4e4d4a97b" />

---

## ✅ 8. Total inventory weight per category

 ```sql
SELECT category,
SUM(weightInGms * availableQuantity) AS total_weight
FROM zepto
GROUP BY category
ORDER BY total_weight DESC;
```
## 📸 Output Screenshots

<img width="392" height="579" alt="Screenshot 2025-08-04 012327" src="https://github.com/user-attachments/assets/912e6e44-b34e-4182-908a-d4e62076d4c6" />
















 








