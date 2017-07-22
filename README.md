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
to check if value matches any value of list. List of values can be set of select statements

value IN (SELECT value FROM table)

IN is shortcut for nested ORs

```
SELECT customer_id, rental_id, return_date 
FROM rental 
WHERE customer_id NOT IN(1,2,13) 
ORDER BY return_date DESC;
```

## LIKE
how to find a name say 
```
SELECT first_name, last_name
FROM customer
WHERE first_name LIKE 'Jen%'
```
uses pattern matching in the second
string with wild card characters
Perent % for any sequence of characters, underscore _ for matching any single character. So _ is 1 char, __ is 2 chars. 

Post gres allows you to do ILIKE, so you can ignore string
ILIKE ignores case

### CHALLENGES
1. How many payment transactions were greater than $5.00?
ans: SELECT COUNT(*) FROM payment WHERE amount > 5;
3,618

2. how many actors have a first name that starts with P?
ans: SELECT COUNT(*) FROM actor WHERE first_name LIKE 'P%';
return 5

3. How many unique districts are our cuspstomers from?
ans: SELECT COUNT( DISTINCT district) FROM address;

4. List of names from those distinct districts in last question
SELECT DISTINCT district FROM address;

5. How many films have a rating of R and cose replacement between 5 and 15?
```
SELECT COUNT(*) FROM film 
WHERE rating = 'R' 
AND replacement_cost BETWEEN 5 AND 15;
```

6. How many films have the word Truman somewhere in the title?
```
SELECT COUNT(title) FROM film 
WHERE title LIKE '%Truman%';
```

## MIN MAX AVG SUM
aggregate functions
```
SELECT ROUND( AVG(amount), 2) FROM payment; // 4.20
SELECT COUNT(*) FROM payment WHERE amount=0.00; // MIN

```

## GROUP BY
divides rows returned into groups
aggregates all info into a single value
```
SELECT col1, aggregate function
FROM table
GROUP BY col1

SELECT customer_id, SUM(amount)
FROM payment
GROUP BY customer_id;

// select column you are grouping by

SELECT staff_id, COUNT(payment)
FROM payment
GROUP BY staff_id;

// counts rows that statement is returning back
// takes all instances of staff id and increments by count

SELECT rating, AVG(rental_rate) 
FROM film
GROUP BY rating;
```

### challenges
We have two staff members id 1 and 2
give bonus to member with most payments

how many payments each staff member handle?
how much was total amount?

```
SELECT staff_id, COUNT(staff_id), SUM(staff_id)
FROM payment
GROUP BY staff_id ORDER BY COUNT(staff_id) DESC;
```

2. Corporate HQ want to know avg replacemnt cost of movies by rating.

```
SELECT rating, ROUND(AVG(replacement_cost), 2)
FROM film
GROUP BY rating ORDER BY AVG(replacement_cost) DESC;
```

3. send coupons to 5 customers who have spend the most amount of money.
get customer ids of top 5 spenders

```
SELECT customer_id, SUM(amount)
FROM payment 
GROUP BY customer_id ORDER BY SUM(amount) DESC
LIMIT 5;
```

## Having
like where clause but for group by condition
examples

```
SELECT rating, AVG(rental_rate)
FROM film
WHERE rating in ('R', 'G', 'PG')
GROUP BY rating
HAVING AVG(rental_rate) < 3; 
```
select and use where clause to get rating no aggregate function
then having to get having avg

challenge
1. customer has at least a total of 40 transaction payments
what customers by customer_id are eligible?

```
SELECT customer_id, COUNT(amount)
FROM payment
GROUP BY customer_id
HAVING COUNT(amount) >= 40;
```

2. when grouped by rating, what movie ratings have an avg rental duration of more than 5 days
```
SELECT rating, ROUND(AVG(rental_duration), 2)
FROM film
GROUP BY rating
HAVING AVG(rental_duration) > 5;
```

[See assessment 1](assessments/assessment1.md)


# Part 2

## AS
for joins, asigns alias name to columns

JOINS
