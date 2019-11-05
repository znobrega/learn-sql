# Relation 1:MANY

- Delete a client that has a order is a problem because you have data depending on
- Orphan data is a big problem
- CASCADE

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
  FOREIGN KEY(customer_id)
    REFERENCES customers(id)
    ON DELETE CASCADE;
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

<h1>JOINS</h1>

![JOINS](https://external-preview.redd.it/M5QHWsp2vgZ-3QDZ4m-qS58lsOUgDNHau8trSFzS8H0.jpg?auto=webp&s=cae9cdc438b71c9025d40dad4650801fdcae1ef8)

#### IMPLICI JOIN (USELESS)

```sql
  SELECT * FROM customers, orders;
```

#### Cross Join

```sql
  SELECT * FROM customers, orders WHERE customers.id = orders.customer_id
```

#### IMPLICIT INNER JOIN

```sql
  SELECT first_name, last_name, order_date, amount
  FROM customers, orders 
    WHERE customers.id = orders.customer_id;

```

# JOIN keyword

### EXPLICIT INNER JOIN

You van use INNER or not

```sql
-- Bad condition
SELECT * FROM customers
INNER JOIN orders
  ON customers.id = orders.id;

SELECT first_name, last_name, order_date, amount FROM customers
JOIN orders
  ON customers.id = orders.id;

-- Correct codition
SELECT * FROM customers
LEFT JOIN orders
  ON customers.id = orders.customer_id; 

SELECT first_name, last_name, order_date, amount FROM customers
JOIN orders
  ON customers.id = orders.customer_id
ORDER BY amount;

SELECT first_name, last_name, order_date, AVG(amount) as average FROM customers
JOIN orders
  ON customers.id = orders.customer_id
GROUP BY last_name, first_name;

SELECT first_name, last_name, order_date, AVG(amount) as average FROM customers
JOIN orders
  ON customers.id = orders.customer_id
GROUP BY orders.customer_id;

SELECT first_name, last_name, order_date, SUM(amount) as total_spent FROM customers
INNER JOIN orders
  ON customers.id = orders.customer_id
GROUP BY orders.customer_id
ORDER BY total_spent DESC;
```

### LEFT JOIN

<p>Take everything from the left table</p>

```sql
  SELECT * FROM customers
  LEFT JOIN orders
    ON customers.id = orders.customer_id; 

  SELECT first_name, last_name, order_date, amount FROM customers
  LEFT JOIN orders
    ON customers.id = orders.customer_id;   

  SELECT 
    first_name, 
    last_name, 
    order_date, 
    IFNULL(SUM(amount), 0) AS total_spent
  FROM customers
  LEFT JOIN orders
    ON customers.id = orders.customer_id
  GROUP BY customers.id
  ORDER BY total_spent DESC;
```

### RIGHT JOIN

```sql
  SELECT * FROM customers
  RIGHT JOIN orders
    ON customers.id = orders.customer_id; 

  SELECT first_name, last_name, order_date, amount FROM customers
  RIGHT JOIN orders
    ON customers.id = orders.customer_id;   

  SELECT 
    first_name, 
    last_name, 
    order_date, 
    IFNULL(SUM(amount), 0) AS total_spent
  FROM customers
  RIGHT JOIN orders
    ON customers.id = orders.customer_id
  GROUP BY customers.id
  ORDER BY total_spent DESC;
```

#### EXERCISE

```sql
  CREATE TABLE students(
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(20) NOT NULL
  );

  CREATE TABLE papers (
    title VARCHAR(100),
    grade INT,
    student_id INT,
    FOREIGN KEY (student_id) 
        REFERENCES students(id)
        ON DELETE CASCADE
  );

  CREATE TABLE papers2 (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(100),
    grade INT,
    student_id INT,
    FOREIGN KEY (student_id) 
        REFERENCES students(id)
        ON DELETE CASCADE
  );

  INSERT INTO students (first_name) VALUES 
  ('Caleb'), ('Samantha'), ('Raj'), ('Carlos'), ('Lisa');

  INSERT INTO papers (student_id, title, grade ) VALUES
  (1, 'My First Book Report', 60),
  (1, 'My Second Book Report', 75),
  (2, 'Russian Lit Through The Ages', 94),
  (2, 'De Montaigne and The Art of The Essay', 98),
  (4, 'Borges and Magical Realism', 89);

  SELECT first_name, title, grade FROM students
  JOIN papers 
    ON students.id = papers.student_id
  ORDER BY grade DESC;

  SELECT 
    first_name, 
    IFNULL(title, 'Missing'),
    IFNULL(grade, 0)
  FROM students
  LEFT JOIN papers
    ON students.id = papers.student_id;

  SELECT 
    first_name,
    IFNULL(AVG(grade), 0) AS average
        FROM students
  LEFT JOIN papers
    ON students.id = papers.student_id
  GROUP BY first_name
  ORDER BY average DESC;

  SELECT 
    first_name,
    IFNULL(AVG(grade), 0) AS average,
    CASE 
      WHEN AVG(grade)>=75 THEN 'PASSING'
      ELSE 'FAILING'
    END AS passing_status
        FROM students
  LEFT JOIN papers
    ON students.id = papers.student_id
  GROUP BY first_name
  ORDER BY average DESC;

```