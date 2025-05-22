# 🍽️ Danny's Diner SQL Case Study

This project is part of the [8-Week SQL Challenge](https://8weeksqlchallenge.com/) by Data With Danny.

---

## 📊 Objectives

Using SQL, I aimed to answer the following questions. Then, used the data I found to see how to improve customer retention and increase revenue.

### ✅ Core Questions
<details><summary><strong>1. What is the total amount each customer spent at the restaurant?</strong></summary>
  
  ```sql
  SELECT
    s.customer_id,
    SUM(m.price) AS total_spent
  FROM sales s
  JOIN menu m ON s.product_id = m.product_id
  GROUP BY s.customer_id;
  ```
## Insights
- In order to solve this question, we need to combine the tables by using **JOIN** so that the prices and menu items can line up.
- Then, we must find the **SUM** of the values in order to see what each customer spent.
- 
</details>

<details><summary><strong>2. How many days has each customer visited the restaurant?</strong></summary>
	
```sql
SELECT
   customer_id,
   COUNT(DISTINCT order_date)
FROM sales
GROUP BY customer_id
```
</details>

<details><summary><strong>3. What was the first item from the menu purchased by each customer?</strong></summary>

```sql
WITH CTE AS(
SELECT
    customer_id,
    order_date,
    product_name,
RANK() OVER(PARTITION BY customer_id ORDER BY order_date ASC)
FROM sales
INNER JOIN menu on sales.product_id = menu.product_id)
SELECT *
FROM CTE
WHERE rank = 1
```
</details>

<details><summary><strong>4. What is the most purchased item on the menu and how many times was it purchased by all customers?</strong></summary>

```sql
SELECT product_name,
COUNT(order_date) as orders
FROM sales
INNER JOIN menu on sales.product_id = menu.product_id
GROUP BY product_name
ORDER BY COUNT(order_date) DESC
LIMIT 1
```
</details>

<details><summary><strong>5. Which item was the most popular for each customer?</strong></summary>

```sql
WITH CTE AS(
SELECT 
    product_name,
    customer_id,
COUNT(order_date) as orders,
RANK() OVER(PARTITION BY customer_id ORDER BY COUNT(order_date) DESC)
FROM sales
INNER JOIN menu on sales.product_id = menu.product_id
GROUP BY 
    product_name,
    customer_id
)
SELECT
    customer_id,
    product_name
FROM CTE
WHERE rank=1
```
</details>

---

## 🧠 Key Insights

- Customer C spends the most and visits most frequently, showing high loyalty.
- Sushi is the most popular item across all customers.
- Most customers tend to order the same item multiple times, indicating strong product preference.
- There is an opportunity to segment customers based on frequency and total spend to create targeted promotions.

---

## 🛠️ Tools Used

- **SQL** – Window functions, joins, aggregations
- **Mode SQL Editor** – To run and test queries
- **Google Sheets / Excel** – For basic visualizations

---

## 📂 Project Structure

