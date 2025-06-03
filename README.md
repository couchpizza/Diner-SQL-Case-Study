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
- In order to solve this question, we need to combine the tables by using **JOIN** so that the prices and menu items can line up. I did this by combining the 'sales' and 'menu.table' using 'product_id' to access the item prices.
- Then, we must find the **SUM** of the values in order to see what each customer spent.
- The results show what each customer spent in total at the restaurant. This information is useful for identifying which customers would respond positively to offers and other loyalty rewards at the restaurant.
</details>

<details><summary><strong>2. How many days has each customer visited the restaurant?</strong></summary>
	
```sql
SELECT
   customer_id,
   COUNT(DISTINCT order_date)
FROM sales
GROUP BY customer_id
```
## Insights
- The most important function here is COUNT(DISTINCT) as it will show exactly how many times each customer (A,B,C) have visited the restaurant without cluttering the data table.
- Customer B is the most frequently returning customer. On its own, this data is still vague, but can help better understand what items keeps this particular customer returning to the restaurant.
</details>

<details><summary><strong>3. What was the first item from the menu purchased by each customer?</strong></summary>

```sql
WITH CTE AS(
SELECT
    customer_id,
    order_date,
    product_name,
ROW NUMBER() OVER(PARTITION BY customer_id ORDER BY order_date ASC) AS row_num
FROM sales
INNER JOIN menu on sales.product_id = menu.product_id)
SELECT *
FROM CTE
WHERE rank = 1
```
## Insights
- Using ROW NUMBER() allows me to retrieve exactly 1 item per customer. The ORDER BY function allows me to see what the customer ordered on the first date they came in.
- This information is important in identifying what items drew the customer to the restaurant in the first place and how we can capitalize on the most alluring menu items.
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
## Insights
- Using the COUNT function in the query, I was able to quantify each time the menu item was ordered as a single number. INNER JOIN was used to combine the product_id on the menu with the amount of sales. Thus, using the COUNT function at the end of the query shows how many times each menu item was purchased.
- In this restaurant the most purchased item was ramen. This information can be usefull in identifying the most popular menu items that can be used for customer retention. That way, marketing strategies can be geared towards selling this particular menu item.
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
## Insights
- This query is written similarly to the previous one to find the data for each customer. The difference in this query is the use of rank=1, which will indicate the most popular item purchased byt each customer.
- The data can be used to create customized deals and rewards for customers based on their preferred menu items to keep bringing them back to the restaurant. The data can also be used to suggest similar menu items to the cusomter if they would like to try new menu items that have a similar taste.
</details>

---

## 🧠 Key Insights



---

## 🛠️ Tools Used

- **SQL** – Window functions, joins, aggregations
- **Mode SQL Editor** – To run and test queries
- **Google Sheets / Excel** – For basic visualizations

---

## 📂 Project Structure

