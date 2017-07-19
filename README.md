# Sql Bootcamp

Notes on SQL course

## From Spreadhseet to Databases

use cases Spreadsheets
- quickly need to chart something else
- reasonable sizes
- untrained people to work 

Databases
- data integrity (change data)
- quickly combine data sets

## SELECT FROM
captialize select by convention for easier reading?
in real case usually you use 100 not * to get all data

## SELECT with DISTINCT
in table, column may contain duplicate values
you jsut want distinct values

SELECT DISTINCT column1, column2
FROM tablename

## SELECT with WHERE
SELECT column1, col2...
FROM table_name
WHERE conditions;

basic logical operators, = > < AND != OR
