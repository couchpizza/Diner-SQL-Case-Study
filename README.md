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

2. How many days has each customer visited the restaurant?
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
5. What is the most purchased item on the menu and how many times was it purchased by all customers?
6. Which item was the most popular for each customer?

### 🔍 Extended Analysis
6. Who are the highest-value customers based on total spend?
7. What is the average number of days between visits for each customer?
8. Which menu items are most frequently ordered overall?
9. Are there any noticeable trends in ordering behavior over time?

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


## 📊 Core Questions & Solutions

<details>
  <summary>🍽️ <strong>1. What is the total amount each customer spent at the restaurant?</strong></summary>

  <br>

  💡 *Business Goal:* Understand how much each customer contributes in revenue.

  ### 🔍 SQL Query:
  ```sql
  SELECT
    s.customer_id,
    SUM(m.price) AS total_spent
  FROM sales s
  JOIN menu m ON s.product_id = m.product_id
  GROUP BY s.customer_id;
```
## insight
- customer c is a big back

</details>
