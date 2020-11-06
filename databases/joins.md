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
FULL join orders o
ON c.customer_id = o.customer_id
```

### Self Join

Table is joined with itself

```sql
SELECT c1.first_name as first_name1, c2.last_name as last_name2, c1.city
FROM customers c1, customers c2
WHERE c1.id <> c2.id -- or !=
ORDER BY c1.city
```
