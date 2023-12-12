# Case Study 1 : Optimizing Online Sports Retail Revenue

## Project Description
~~In this project, we'll analyze the product data of an online sports clothing company and develop recommendations to help the company maximize its revenue. The information includes prices, discounts, revenue, ratings, reviews, product descriptions, and website traffic.~~

Sports clothing and athleisure attire is a huge industry, worth approximately $193 billion in 2021 with a strong growth forecast over the next decade!

In this project, we play the role of a product analyst for an online sports clothing company. The company is specifically interested in how it can improve revenue. We will dive into product data such as pricing, reviews, descriptions, and ratings, as well as revenue and website traffic, to produce recommendations for its marketing and sales teams.

The database provided to us, sports, contains five tables, with product_id being the primary key for all of them:
*<p align="center"> ![Database](https://github.com/macababbadcherry/Learning-SQL/assets/148540172/16bc34ce-47eb-49fa-9eaf-dcca5d301f1a) </p>*

Note that the project description and tasks of this case study has been sourced from [[DataCamp] Optimizing Online Sports Retail Revenue](https://app.datacamp.com/learn/projects/optimizing_online_revenue). The dataset can be obtained from [Kaggle](https://www.kaggle.com/datasets/irenewidyastuti/datacamp-optimizing-online-sports-retail-revenue).

## Project Tasks
This project involves 9 tasks that require the use of SQL to analyze and optimize the revenue of an online sports clothing company. 

1. Counting missing values
2. Nike vs Adidas pricing
3. Labeling price ranges
4. Average discount by brand
5. Correlation between revenue and reviews
6. Ratings and reviews by product description length
7. Reviews by month and brand
8. Footwear product performance
9. Clothing product performance

## Analysis and Insights

### 1. Counting missing values
Count the total number of products, along with the number of non-missing values in description, listing_price, and last_visited.
```SQL
SELECT
  COUNT(*) AS total rows,
  COUNT(i.description) AS count_description,
  COUNT(f,listring_price) AS count_listing_price,
  COUNT(t.last_visited) AS count_last_visited
FROM info i
JOIN finance f
ON i.product_id = f.product_id
JOIN traffic t
ON i.product_id = t.product_id
```
**Steps:**
- Use `JOIN` to merge `info` table with `finance` and `traffic`, matching on `product id`.
- To determine the total number of the required fields, we use `COUNT`.

**Results:**

### 2. Nike vs Adidas pricing
How do the price points of Nike and Adidas products differ?
