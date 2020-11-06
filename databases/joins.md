# Joins

There are different types of SQL joins:

* Inner
* Left
* Right
* Full/Outter
* Self

![venns](https://images.squarespace-cdn.com/content/v1/5732253c8a65e244fd589e4c/1464122797709-C2CDMVSK7P4V0FNNX60B/ke17ZwdGBToddI8pDm48kMjn7pTzw5xRQ4HUMBCurC5Zw-zPPgdn4jUwVcJE1ZvWEV3Z0iVQKU6nVSfbxuXl2c1HrCktJw7NiLqI-m1RSK4p2ryTI0HqTOaaUohrI8PIO5TUUNB3eG_Kh3ocGD53-KZS67ndDu8zKC7HnauYqqk/image-asset.png?format=300w)

## Types

Imagine we have two tables, one for `customers` and other for `orders` which has a column `customer_id` creating a _one-to-many_ relation.

### Inner Join

Suppose we want to get a list of those customers who placed an order and details of the order they placed.

Inner join would return records at the intersection of two tables.

```sql
SELECT first_name, last_name, order_date, order_amount
FROM customers c
INNER JOIN orders o
ON c.customer_id = o.customer_id

```

### Left Join

Suppose we want to simply append information about orders, whether a customer placed an order or not.

```sql
SELECT first_name, last_name, order_date, order_amount
FROM customers c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
```

And if we wanted to know which customers have not placed an order:

```sql
SELECT first_name, last_name, order_date, order_amount
FROM customers c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
WHERE order_date is NULL
```

### Right Join

Mirror version of the left join, in our case, it would allow to get a list of all orders, appended with customer information.

```sql
SELECT first_name, last_name, order_date, order_amount
FROM customers c
RIGHT JOIN orders o
on c.customer_id = o.customer_id
```

### Full/Outter Join

Finally, for a list of all records for both tables.

```sql
SELECT first_name, last_name, order_date, order_amount
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id -- If we don't specify how to relate tables, it will do a cartesian product A x B
```

### Self Join

Table is joined with itself

```sql
SELECT c1.first_name as first_name1, c2.last_name as last_name2, c1.city
FROM customers c1, customers c2
WHERE c1.id <> c2.id -- or !=
ORDER BY c1.city
```

## Joining Three or more tables

### Does Join order matter?

Keep in mind that SQL is a __non-procedural language__, meaning that you describe what you want to retrieve and which database objects need to be involved, but it's up to the database server to determine how to best execute your query.

Using statistic gathered from your database objects, the server must pick one of three tables as a starting point (the chosen table is thereafter known as the __driving table__), and then decide in which order ot join the remaining tables.

__The order in which tables appear in your `FROM` clause is not significant__.

If, however, you believe the tables in your query should always be joined in a particular order, you can place the tables in the desired order and specify it with a specific database server keyword, which in MySQL case is `STRAIGHT_JOIN`.

```sql
SELECT STRAIGHT_JOIN a.account_id, c.fed_id, e.fname, e.lname
FROM employee e INNER JOIN account a
  ON e.emp_id = a.open_emp_id
  INNER JOIN customer c
  ON a.cust_id = c.cust_id
WHERE c.cust_type_cd = 'B';
```

### Subqueries as Tables

```sql
SELECT a.account_id, a.cust_id, a.open_date, a.product_cd
FROM account a INNER JOIN
  (
    SELECT emp_id, assigned_branch_id
    FROM employee
    WHERE start_date < '2007-01-01'
      AND (title = 'Teller' OR title = 'Head Teller')
  ) e
  ON a.open_emp.id = e_emp_id
  INNER JOIN
    (
      SELECT branch_id
      FROM branch
      WHERE name = 'Woburn Branch' 
    ) b
    ON e.assigned_branch_id = b.branch_id;
```
