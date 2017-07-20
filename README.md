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

```
SELECT customer
WHERE first_name = 'Tim' AND last_name='John'
basic logical operators, = > < AND != OR
```

## COUNT
COUNT statement, counts where condition was true
```
SELECT COUNT(DISTINCT amount) FROM payment;
```

## LIMIT
limit rows back
```
SELECT * FROM customer LIMIT 1;
```

## ORDER BY
sort rows in either ascending or descending
```
SELECT first_name, last_name FROM customer ORDER BY first_name ASC;

// also by multiple columns
SELECT first_name, last_name FROM customer ORDER BY first_name ASC, last_name DESC;
```

## BETWEEN
value BETWEEN low AND high
```
SELECT customer_id, amount, payment_date FROM payment
WHERE payment_date BETWEEN '2007-02-07' AND '2007-02-15';

// you can use numbers or strings
```

## IN

## LIKE
