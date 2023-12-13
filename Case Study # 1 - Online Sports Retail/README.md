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
  COUNT(*) AS total_rows,
  COUNT(i.description) AS count_description,
  COUNT(f.listing_price) AS count_listing_price,
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

```SQL
SELECT brand, CAST(listing_price AS INT), COUNT(*)
FROM brands b
JOIN finance f 
ON b.product_id = f.product_id
WHERE listing_price > 0 
GROUP BY brand, listing_price
ORDER BY listing_price DESC
```

### 3. Labeling price ranges
```SQL
SELECT brand, 
       COUNT(f.*), 
       SUM(revenue) AS total_revenue,
       CASE WHEN listing_price < 42 THEN 'Budget'
            WHEN listing_price >= 42 AND listing_price < 74 THEN 'Average'
            WHEN listing_price >= 74 AND listing_price < 129 THEN 'Expensive'
            ELSE 'Elite' 
            END AS price_category
FROM brands b
JOIN finance f
ON b.product_id = f. product_id
WHERE brand IS NOT NULL
GROUP BY brand, price_category
ORDER BY total_revenue DESC
```

### 4. Average discount by brand

```SQL
SELECT brand, AVG(discount)*100 AS average_discount
FROM brands b
JOIN finance f
ON b.product_id = f.product_id
WHERE brand IS NOT NULL
GROUP BY brand
```

### 5. Correlation between revenue and reviews

```SQL
SELECT CORR(reviews, revenue) AS review_revenue_corr
FROM reviews r
JOIN finance f
ON r.product_id = f.product_id
```

### 6. Ratings and reviews by product description length
```SQL
SELECT TRUNC(LENGTH(description)/100.0)*100 AS description_length,
ROUND(AVG(CAST(rating as numeric)),2) AS average_rating
FROM info i
JOIN reviews r
ON i.product_id = r.product_id
WHERE description IS NOT NULL
GROUP BY description_length
ORDER BY description_length
```

### 7. Reviews by month and brand

```SQL
SELECT brand,
       DATE_PART('month', last_visited) as month,
       COUNT(r.*) as num_reviews
FROM traffic t
JOIN reviews r
ON t.product_id = r.product_id
JOIN brands b
ON t.product_id = b.product_id
GROUP BY brand, month
HAVING brand IS NOT NULL
  AND DATE_PART('month', last_visited) IS NOT NULL
ORDER BY brand, month
```

### 8. Footwear product performance

```SQL
WITH footwear AS
(
    SELECT description, revenue
    FROM info i
    JOIN finance f
    ON i.product_id = f.product_id
    WHERE description ILIKE '%shoe%' 
        OR description ILIKE '%trainer%'
        OR description ILIKE'%foot%'
        AND description IS NOT NULL
)

SELECT COUNT(*) as num_footwear_products, 
       percentile_disc(0.5) WITHIN GROUP (ORDER BY revenue) AS median_footwear_revenue
FROM footwear
```
### 9. Clothing product performance
   
```SQL
WITH footwear AS
(
    SELECT description, revenue
    FROM info i
    JOIN finance f
    ON i.product_id = f.product_id
    WHERE description ILIKE '%shoe%' 
        OR description ILIKE '%trainer%'
        OR description ILIKE'%foot%'
        AND description IS NOT NULL
)

SELECT COUNT(i.*) AS num_clothing_products,
       percentile_disc(0.5) WITHIN GROUP (ORDER BY f.revenue) AS median_clothing_revenue
FROM info i
JOIN finance f
ON i.product_id = f.product_id
WHERE description NOT IN (SELECT description FROM footwear)

```

