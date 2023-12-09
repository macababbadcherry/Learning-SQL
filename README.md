# Learning-SQL
This repository serves as a directory for my work and exercises, showcasing my growth in SQL.

Cetifications: insert link

# I. Introduction to SQL

## Relational Databases
### Databases
Databases store and organize data electronically. It can store much more data than spreadsheet applications, and storage is more secure due to encryption. A relational database defines relationships between tables of data inside the database. Most of the relational databases use a language called SQL, or “Structured Query Language." SQL is the most widely used programming language for creating, querying, and updating relational databases.

### Tables
Tables are the main building blocks of databases. The rows and columns are referred as records and fields, respectively. A record is a row that holds data on an individual observation. A field is a column that holds one piece of information about all records. A unique identifier, sometimes called a "key," is just what it sounds like: a unique value which identifies a record so that it can be distinguished from other records in the same table. 

### Data Types
Listed below are the data types.
  1. String. It is a sequence of characters such a letters or punctuations where `VARCHAR` is very commonly used for storing strings.
  2. Integers. It store whole numbers where `INT`, a common SQL integer data type, can store numbers from less than negative two billion to more than positive two billion.
  3. Float. It stores numbers that include a fractional part where the `NUMERIC` data type can store floats which have up to 38 digits total - including those before and after the decimal point.

//Schemas are often referred to as "blueprints" of databases. A schema shows a database's design, such as what tables are included in the database and any relationships between its tables. A schema also lets the reader know what data type each field can hold. The schema for our library database shows the VARCHAR data type is used for strings like book title, author, and genre. We can also see that the patrons table is related to the checkouts table, but not the books table.

## Querying
Query is a request of data from the database. 

### Writing Queries 
Presented are few more commonly used keyword in SQL.
1. `AS`. Use *aliasing* to rename columns.
2. `DISTINCT`. Return a list of unique values.
3. `CREATE VIEW`. A view is a virtual table that is the result of a saved SQL  `SELECT` statement. It is the query code that is stored for future use.

## SQL Flavors
PostgreSQL and SQL Server are the two popular SQL servers.
1. PostgreSQL is a free and open-source relational database system
2. SQL Server is also a relational database system which comes in both free and enterprise versions. It was created by Microsoft.

### Comparing PostgreSQL and SQL Server
PostgreSQL: `SELECT id, name
FROM employees --
LIMIT 2; `

SQL Server: `SELECT TOP(2) id, name
FROM employees `

# II. Intermediate SQL
## A. Selecting Data
**PostgreSQL**.The keywords are as follows:
1. `COUNT()`. Counts the number of records with a value in a field
2. `DISTINCT`. Removes duplicates to return only unique values
3. `COUNT()` with `DISTINCT`. Count the number of unique values in a field.

**Query Execution**. *It makes sense that SQL needs to know where to* `SELECT` *data* `FROM` *before it can* `LIMIT` *the results.*  SQL code is processed differently than other programming languages in that you need to let the processor know where to pull the data from before making selections.

It's essential to know your code's order of execution compared to the order it is written in to understand what results you'll get from your query and how to fix any errors that may come up. Knowing processing order is especially useful when debugging and aliasing fields and tables.

Most common errors are misspelling, incorrect capitalization, and incorrect or missing punctuation especially commas.

**SQL Formatting**. Adhering to SQL style guides allows for easier collaboration between peers. Having clean and readable code is highly valued in the community and a professional setting and will make things easier for anyone wanting to understand or debug our queries.

In dealing with non-standard filed names, put non-standard filed names in double-quotes.

## B. Filtering Records
**Filteting numbers and exact text**. `WHERE` allows us to focus on only the data relevant to our business questions. The comparison operators we can use with WHERE to filter numbers are 
- `>` greater than (that also means after),
- `<` less than (that also means before),
- `=` equal to,
- `<>` greater than or equal to, less than or equal to, and not equal to.

`WHERE` can also filter string values. Use single quote.

 To enhance our filters when using WHERE by adding multiple criteria. we can use the keywords, `OR`, `AND`, and `BETWEEN`.
- `OR` is used if we need to satisfy at least one condition.
- `AND` is used if we need to satisfy all criteria.
- `BETWEEN` keyword provides a valuable shorthand for filtering values within a specified range.
  
If a query has multiple filtering conditions, we will need to enclose the individual clauses in parentheses to ensure the correct execution order; otherwise, we may not get the expected results.

**Filtering text**. This is filtering a pattern in a `WHERE` clause  rather than specific text. We'll be introducing three more SQL keywords into our vocabulary to help us achieve this: `LIKE`, `NOT LIKE`, and `IN`.
- `LIKE`. It is used to search for a pttern in a field. We use a wildcard as a placeholder for some other values to accomplish this.  The percent wildcard will match zero, one, or many characters in the text.  The underscore wildcard will match a single character.
- `NOT LIKE`. It is used to find records that don't match the specified pattern. 
- `IN`. It allows us to specify multiple values in a WHERE clause, making it easier and quicker to set numerous OR conditions.

**Filtering null values**. In SQL, NULL represents a missing or unknown value. Why is this useful? In the real world, our databases will likely have empty fields either because of human error or because the information is not available or is unknown. Knowing how to handle these fields is essential as they can affect any analyses we do.
- `IS NULL`One quick way to see how much of our data is missing is by using `IS NULL` with the WHERE clause.
- `IS NOT NULL`. This is to filter out/exclude missing values, so we only get results that are not NULL
  
## C. Aggregate Functions
**Summarizing data**. One way to do this is to summarize the data using SQL's aggregate functions. We already know one aggregate function, COUNT(). We'll now learn four new aggregate functions, allowing us to find the average, sum, minimum, and maximum of a specified field. These aggregate functions come after SELECT, exactly like COUNT().
- `AVG`. It gives us the average value. 
- `SUM`. It returns to the result of adding the values.
- `MIN`. It returns the lowest value
- `MAX`. It returns the highest value.

Average and sum are the two aggregate functions we can only use on numerical fields since they require arithmetic. We can use count, minimum, and maximum with non-numerical fields. 

`ROUND(number_to_round, decimal_places)`. It can only be used with numerical fields and is rounding a number to a specified decimal where the second parameter is optional. We could also pass a negative number as the second parameter and still get a result. 

**Aggregate functions and arithmetic.** The key difference is that aggregate functions, like SUM, perform their operations on the fields vertically while arithmetic adds up the records horizontally.

## D. Sorting and Grouping

**Sorting results.** Sorting results means we want to put our data in a specific order. It's another way to make our data easier to understand by quickly seeing it in a sequence. `ORDER BY` is a keyword used in this action. 

`ORDER BY`. It is used to sort results of one or more fields.
- `DESC`. It is used to sort the results in descending order. 
-  Multiple fileds. It will sort by the first field specified, then sort by the next, etc.

**Grouping results.**  In the real world, we'll often need to summarize data for a particular group of results. SQL allows us to group with the  `GROUP BY` clause.

`GROUP BY`. It is commonly used is commonly used with aggregate functions to provide summary statistics, particularly when only grouping a single field, certification, and selecting multiple fields, certification and title. 
- Multiple fields. The order in which we write the fields affects how the data is grouped. The query here selects and groups certification and language while aggregating the title.
- with `ORDER BY`. It is used to group our results, make a calculation, and then order our results (sorting anf grouping).

**Filtering grouped data.** In SQL, we can't filter aggregate functions with WHERE clauses. Groups have their own special filtering word: `HAVING`. 

`HAVING` vs `WHERE` WHERE filters individual records while HAVING filters grouped records. 
- "What films were released in the year 2000?". This question does not indicate any sort of grouping. It asks to see only the titles from a specific year and can therefore be written as SELECT title, FROM films, WHERE release year equals 2000.
- "In what years was the average film duration over two hours?". Recall the aggregate function will convert the duration values into one average value.

## E. Summary
- Selecting with `COUNT()` and `LIMIT`
- Filtering with `WJERE`, `BETWEEN`, `AND`, `OR`, `LIKE`, `NOT LIKE`, `IN`, `%`, `_`, `IS NULL`, `IS NOT NULL`
- `ROUND()` and aggregate functions
- Sorting and grouping with `ORDER BY`, `DESC`, `GROUP BY` `HAVING`
- Comparison operators
- Arithmetic



# III. Joining Data in SQL (PostgreSQL)
**Joining data**. Joining  is an essential skill which enables us to draw information from separate tables together into a single, meaningful set of results.

## A. Introducing Inner Joins 
 **`INNER JOIN`.** Looks for records in both tables which match on a given field.
  a.  `ON`
  b. `USING`. When joining on two identical column names, we can employ the USING command followed by the shared column name in parentheses. Here, since the join field is named "country" in both tables, we can use USING.

Syntax Example:
SELECT name, e.year, fertility_rate, unemployment_rate
FROM countries AS c
INNER JOIN populations AS p
ON c.code = p.country_code
INNER JOIN economies AS e
ON p.year = e.year AND c.code = e.code;

Syntax for performing an INNER JOIN. When selecting columns that exist in both tables, such as "country" and "continent", the table-dot-column_name format must be used to avoid a SQL error. 
1. After FROM, we list the left table, followed by the INNER JOIN keyword and the right table.
2. We then specify the field to match the tables on, using the ON keyword. Here, we use the "country" field.
3. Lastly, we add SELECT at the start of the query and choose the fields we want returned.

## B. Outer Joins, Cross Joins and Self Joins

**Outer joins.** It can obtain records from other tables, even if matches are not found for the field being joined on.
- `LEFT JOIN`. It will return all records in the left table, and those records in the right table that match on the joining field provided. Note that `LEFT JOIN` can also be written as `LEFT OUTER JOIN` in SQL. 
- `RIGHT JOIN`. All records are retained from right table, even when id doesn't find a corresponding match in left table.  Null values are returned for the left value field in records that do not find a match. `RIGHT JOIN` can also be written as `RIGHT OUTER JOIN` in SQL.
- `FULL JOIN`. It combines a `LEFT JOIN` and a `RIGHT JOIN`. Note that the keyword `FULL OUTER JOIN` can also be used to return the same result.

A RIGHT JOIN can always be re-written as a LEFT JOIN. Because we typically type from left to right, LEFT JOIN feels more intuitive to most users when constructing queries.

**`CROSS JOIN`.** It creates all possible combinations of two tables. Note that the syntax is very minimal, and we do not specify ON or USING with CROSS JOIN. 

## C. Set Theory for SQL Joins
**Set operations.** It is a new way of joining data: set operations. SQL has three main set operations, UNION, INTERSECT and EXCEPT. For all set operations, the number of selected columns and their respective data types must be identical. The result will only use field names (or aliases, if used) of the first SELECT statement in the query.

- `UNION`. The operator takes two tables as input, and returns all records from both tables. If two records are identical, `UNION` only returns them once.
- `UNION ALL`. The operator takes two tables and returns all records from both tables, including duplicates.

Syntax
SELECT *
FROM left_table
UNION / UNION ALL
SELECT *
FROM right_table
UNION / UNION ALL

- `INTERSECT`. It takes two tables as input, and returns only the records that exist in both tables.

