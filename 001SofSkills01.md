# SQL - Joins and Aggregations


## Contents:

  - [1. SQL - Structured Query Language](#1-sql---structured-query-language)
  - [2. SQL Clauses](#2-sql-clauses)
  - [3. ```JOIN``` Clause](#3-join-clause)
    - [3.1. ```INNER JOIN``` Clause](#31-inner-join-clause)
    - [3.2. ```LEFT JOIN``` Clause](#32-left-join-clause)
    - [3.3. ```RIGHT JOIN``` Clause](#33-right-join-clause)
    - [3.4. ```FULL JOIN``` Clause](#34-full-join-clause)
  - [4. Aggregate Functions](#4-aggregate-functions)
    - [4.1. ```COUNT()```](#41-count)
    - [4.2. ```SUM()```](#42-sum)
    - [4.3. ```AVG()```](#43-avg)
    - [4.4. ```MAX()```](#44-max)
    - [4.5. ```MIN()```](#45-min)
  - [5. References](#5-references)

<hr>
<br>

## 1. SQL - Structured Query Language

**SQL** stands for **Structured Query Language** which is a data query language designed to **create, manage and query a structured database** stored in a **relational database management system (RDBMS)**. It is particularly useful in handling structured data incorporating relations among entities and variables within them.

A database is a collection of one or more tables. Each of the table in a database is identified by a name. Each Table have two main structure within them, **Fields** which generally called columns and **Records** which are generally known as rows.

Consider following table for example:

<br>

**Customers:**

CustomerID|CustomerName|ContactNumber
----------|------------|--------------
UP32AA0001|Arjun Singh|9412345678
KA01AB0231|Vishal Dhruva|9838987654
SK01CA3421|Pragya Lepcha|8421163264
WB74AA9823|Shahbaz Chowdhury|9451443322

<br>

Above table has **3 Fields** (*CustomerID*, *CustomerName* and *ContactNumber*) and **4 Records**

<br>

## 2. SQL Clauses:

SQL has many **frequently used in-built functions** available which are called **Clauses**. Clauses help us query, filter, analyze and manipulate databases and tables efficiently. Some examples of Clause are: ```WHERE```, ```AND```, ```OR```, ```LIKE```, ```TOP```, ```LIKE```, etc.

<br>

## 3. ```JOIN``` Clause:

```JOIN``` is a SQL clause which is used to combine data from two or more tables based on a common field between them. The different ```JOIN``` clause are as follows:

1. ```INNER JOIN``` <br> ![INNER JOIN Clause](https://www.w3schools.com/sql/img_innerjoin.gif) | 2. ```LEFT JOIN``` <br> ![LEFT JOIN Clause](https://www.w3schools.com/sql/img_LEFTjoin.gif)
-------------------------------------|---------------------------------

<br>

3. ```RIGHT JOIN``` <br> ![RIGHT JOIN Clause](https://www.w3schools.com/sql/img_rightjoin.gif) | 4. ```FULL JOIN``` <br> ![FULL JOIN Clause](https://www.w3schools.com/sql/img_fulljoin.gif)
-------------------------------------|---------------------------------

<br><br>

To understand these clauses, consider following two tables:

<br>

**Student:**

ROLL_NO|NAME|ADDRESS|PHONE|AGE
-------|----|-------|-----|---
1|Harsh|Delhi|9823041567|18
2|Pratik|Bihar|9723014765|19
3|Priyanka|Siliguri|7787435210|20
4|Deep|Balrampur|9838584326|18
5|Shantnu|Kolkata|9415283437|19
6|Dhanraj|Agra|9451993258|20
7|Rohit|Rohtak|7834876242|18
8|Niraj|Alipur|7899435897|19

<br>

**StudentCourse:**

COURSE_ID|ROLL_NO
---------|-------
1|1
2|2
2|3
3|4
1|5
4|9
5|10
4|11

<br>

### 3.1. ```INNER JOIN``` Clause:

The ```INNER JOIN``` clause selects all rows from both tables as long as there is a match between the columns.

**Syntax:**

```
SELECT table1.column1,table1.column2,table2.column1,....
FROM table1 
INNER JOIN table2
ON table1.matching_column = table2.matching_column;
```
**Example:**

If there are records in the "Student" table that do not have matches in "StudentCourse", these orders will not be shown!
```
SELECT StudentCourse.COURSE_ID, Student.NAME, Student.AGE FROM Student
INNER JOIN StudentCourse
ON Student.ROLL_NO = StudentCourse.ROLL_NO;
```
**Output:**

COURSE_ID|NAME|AGE
---------|----|---
1|Harsh|18
2|Pratik|19
2|Priyanka|20
3|Deep|18
1|Shantnu|19

<br>

### 3.2. ```LEFT JOIN``` Clause:

```LEFT JOIN``` is one of the outer joins that returns all the rows of the table on the left side of the join and matching rows for the table on the right side of join. The case in which rows of the left side for which there is no matching row on right side, the result will contain null.

**Syntax:**

```
SELECT table1.column1,table1.column2,table2.column1,....
FROM table1 
LEFT JOIN table2
ON table1.matching_column = table2.matching_column;
```
**Example:**

```
SELECT Student.NAME,StudentCourse.COURSE_ID 
FROM Student
LEFT JOIN StudentCourse 
ON StudentCourse.ROLL_NO = Student.ROLL_NO;
```

**Output:**

NAME|COURSE_ID
----|---------
Harsh|1
Pratik|2
Priyanka|2
Deep|3
Shantnu|1
Dhanraj|*NULL*
Rohit|*NULL*
Niraj|*NULL*

<br>

### 3.3. ```RIGHT JOIN``` Clause:

```RIGHT JOIN``` is one of the outer joins that returns all the rows of the table on the right side of the join and matching rows for the table on the left side of join. The case in which rows of the right side for which there is no matching row on left side, the result will contain null.

**Syntax:**

```
SELECT table1.column1,table1.column2,table2.column1,....
FROM table1 
RIGHT JOIN table2
ON table1.matching_column = table2.matching_column;
```
**Example:**

```
SELECT Student.NAME,StudentCourse.COURSE_ID 
FROM Student
RIGHT JOIN StudentCourse 
ON StudentCourse.ROLL_NO = Student.ROLL_NO;
```

**Output:**

NAME|COURSE_ID
----|---------
Harsh|1
Pratik|2
Priyanka|2
Deep|3
Shantnu|1
*NULL*|4
*NULL*|5
*NULL*|4

<br>

### 3.4. ```FULL JOIN``` Clause:

```FULL JOIN``` is an outer join that creates the result by combining result of both ```LEFT JOIN``` and ```RIGHT JOIN```. The result will contain all the rows from both the tables and the rows for which there is no matching, the result will contain NULL values.

**Syntax:**

```
SELECT table1.column1,table1.column2,table2.column1,....
FROM table1 
FULL JOIN table2
ON table1.matching_column = table2.matching_column;
```
**Example:**

```
SELECT Student.NAME,StudentCourse.COURSE_ID 
FROM Student
FULL JOIN StudentCourse 
ON StudentCourse.ROLL_NO = Student.ROLL_NO;
```

**Output:**

NAME|COURSE_ID
----|---------
Harsh|1
Pratik|2
Priyanka|2
Deep|3
Shantnu|1
Dhanraj|*NULL*
Rohit|*NULL*
Niraj|*NULL*
*NULL*|4
*NULL*|5
*NULL*|4

<br>
<hr>
<br>

## 4. Aggregate Functions:

An aggregate function is a deterministic function that performs a calculation on a set of data, and returns a single value as output. Except for ```COUNT(*)```, aggregate functions ignore null values and are often used with the ```GROUP BY``` clause of the ```SELECT``` statement. They are mainly used to get the summary of the data.

There are five most basic aggregate functions:

1. ```COUNT()```
2. ```SUM()```
3. ```AVG()```
4. ```MAX()```
5. ```MIN()```

<br>

To understand all these aggregate functions, following sample table will be used:

**Chocolates:**

PRODUCT|COMPANY|QUANTITY|RATE|COST
-------|-------|--------|----|----
Dairy Milk|Cadbury|2|10|20
KitKat|Nestle|3|25|75
Bournville|Cadbury|2|30|60
Kisses|Hershey's|5|10|50
Milky Bar|Nestle|2|20|40
Caramilk|Cadbury|3|25|75
Creme Egg|Cadbury|5|30|150
5 Star|Cadbury|3|10|30
Bar One|Nestle|2|25|50
Milk Chocolate|Hershey's|4|30|120

<br>

### 4.1. ```COUNT()```:

```COUNT()``` is an aggregate function used to count the number of rows in a database. It can work on both numeric and non-numeric data types. It uses the COUNT(\*) that returns the count of all the rows in a specified table while considering duplicates and Nulls.

**Syntax:**
```
COUNT ( { [ [ ALL | DISTINCT ] expression ] | * } )
```

**Example:**
```
SELECT COUNT(*)
FROM Chocolates;
```
**Output:**
```
10
```
<br>

### 4.2. ```SUM()```:

```SUM()``` is an aggregate function that returns the sum of all the values, or only the ```DISTINCT``` values, in the expression. It can only be used with numeric columns and it ignores Null values.

**Syntax:**
```
SUM ( [ ALL | DISTINCT ] expression )
```

**Example:**
```
SELECT SUM(COST)
FROM Chocolates;
```
**Output:**
```
670
```
<br>

### 4.3. ```AVG()```:

```AVG()``` is an aggregate function that is used to calculate the average value of the numeric type. It returns the average of all non-Null values.

**Syntax:**
```
AVG ( [ ALL | DISTINCT ] expression )
```

**Example:**
```
SELECT AVG(COST)
FROM Chocolates;
```
**Output:**
```
67.00
```
<br>

### 4.4. ```MAX()```:

```MAX()``` is an aggregate function that is used tused to find the maximum value of a certain column. It determines the largest value of all selected values of a column.

**Syntax:**
```
MAX( [ ALL | DISTINCT ] expression )
```

**Example:**
```
SELECT MAX(RATE)
FROM Chocolates;
```
**Output:**
```
30
```
<br>

### 4.5. ```MIN()```:

```MIN()``` is an aggregate function that is used tused to find the minimum value of a certain column. It determines the smallest value of all selected values of a column.

**Syntax:**
```
MIN( [ ALL | DISTINCT ] expression )
```

**Example:**
```
SELECT MIN(RATE)
FROM Chocolates;
```
**Output:**
```
10
```
<br>

## 5. References:

1. [W3Schools | SQL](https://www.w3schools.com/sql/default.asp)
2. [GeeksForGeeks | SQL | Join (Inner, Left, Right and Full Joins)](https://www.geeksforgeeks.org/sql-join-set-1-inner-left-right-and-full-joins/)
3. [JavaTPoint | SQL Aggregate Functions](https://www.javatpoint.com/dbms-sql-aggregate-function)
4. [Microsoft Docs | SQL Docs](https://www.javatpoint.com/dbms-sql-aggregate-function)