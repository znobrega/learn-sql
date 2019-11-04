# Relation

CUSTOMERS, ORDER

```sql
CREATE TABLE customers(
  id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  first_name VARCHAR(20) NOT NULL,
  last_name VARCHAR(20) NOT NULL,
  email VARCHAR(20) NOT NULL
);

CREATE TABLE orders(
  id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  order_date DATE NOT NULL,
  amount DECIMAL(8,2) NOT NULL,
  customer_id INT NOT NULL,
  FOREIGN KEY(customer_id) REFERENCES customers(id)
);

INSERT INTO customers (first_name, last_name, email) 
VALUES ('Boy', 'George', 'george@gmail.com'),
       ('George', 'Michael', 'gm@gmail.com'),
       ('David', 'Bowie', 'david@gmail.com'),
       ('Blue', 'Steele', 'blue@gmail.com'),
       ('Bette', 'Davis', 'bette@aol.com');
       
INSERT INTO orders (order_date, amount, customer_id)
VALUES ('2016/02/10', 99.99, 1),
       ('2017/11/11', 35.50, 1),
       ('2014/12/12', 800.67, 2),
       ('2015/01/03', 12.50, 2),
       ('1999/04/11', 450.25, 5);
```

#### JOIN's

![JOINS](https://external-preview.redd.it/M5QHWsp2vgZ-3QDZ4m-qS58lsOUgDNHau8trSFzS8H0.jpg?auto=webp&s=cae9cdc438b71c9025d40dad4650801fdcae1ef8)

#### IMPLICI JOIN (USELESS)

```sql
  SELECT * FROM customers, orders;
```

#### Cross Join

```sql
  SELECT * FROM customers, orders WHERE customers.id = orders.customer_id
```

### IMPLICIT INNER JOIN

```sql
  SELECT first_name, last_name, order_date, amount
  FROM customers, orders 
    WHERE customers.id = orders.customer_id;

```

# JOIN keyword

### EXPLICIT INNER JOIN

```sql
SELECT * FROM customers
JOIN orders
  ON customers.id = orders.id;

SELECT first_name, last_name, order_date, amount FROM customers
JOIN orders
  ON customers.id = orders.id;
```



