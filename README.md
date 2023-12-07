# Learning-SQL
This repository serves as a directory for my work and exercises, showcasing my growth in SQL.

Cetifications: insert link

# Introduction to SQL

## Relational Databases
### Databases
Databases store and organize data electronically. It can store much more data than spreadsheet applications, and storage is more secure due to encryption. A relational database defines relationships between tables of data inside the database. Most of the relational databases use a language called SQL, or “Structured Query Language." SQL is the most widely used programming language for creating, querying, and updating relational databases.

### Tables
Tables are the main building blocks of databases. The rows and columns are referred as records and fields, respectively. A record is a row that holds data on an individual observation. A field is a column that holds one piece of information about all records. A unique identifier, sometimes called a "key," is just what it sounds like: a unique value which identifies a record so that it can be distinguished from other records in the same table. 

### Data Types
Listed below are the data types.
  1. String. It is a sequence of characters such a letters or punctuations where VARCHAR is very commonly used for storing strings.
  2. Integers. It store whole numbers where INT, a common SQL integer data type, can store numbers from less than negative two billion to more than positive two billion.
  3. Float. It stores numbers that include a fractional part where the NUMERIC data type can store floats which have up to 38 digits total - including those before and after the decimal point.

//Schemas are often referred to as "blueprints" of databases. A schema shows a database's design, such as what tables are included in the database and any relationships between its tables. A schema also lets the reader know what data type each field can hold. The schema for our library database shows the VARCHAR data type is used for strings like book title, author, and genre. We can also see that the patrons table is related to the checkouts table, but not the books table.

## Querying

### Query 
Query is a request of data from the database. 

### Writing Queries 
1. `#AS`. Aliasing
