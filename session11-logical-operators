# Logical operators

- =
- !=
- LIKE and NOT LIKE
- AND or &&
- OR or ||
- BETWEEN 244 AND 2000
- NOT BETWEEN 244 AND 2000
  <p>To make comparitions with date, is important to use `CAST('2019-01-02' AS DATETIME)`</p>
- IN and NOT IN
  <p>work like multiple OR's coditions</p>

```sql
case doesn't matter 
'A' = 'a'

SELECT * FROM books WHERE author_lname = 'Eggers' AND released_year > 2000 AND title LIKE '%novel%';
```

#### CASE STATEMENT

Case is the if/else of SQL. 
`WHEN` receives a codition, `THEN` gives the name, `ELSE` do something else
```sql
SELECT title, released_year,
  CASE 
    WHEN relesed_year >= 200 THEN 'Mordern Lit'
    ELSE '2 
FROM books;  

SELECT title, stock_quantity, 
  CASE 
    WHEN stock_quantity BETWEEN 0 AND 50 THEN '*'
    WHEN stock_quantity BETWEEN 51 AND 100 THEN '**'
    ELSE '***' 
  END AS level 
FROM books;

SELECT title, stock_quantity, 
  CASE 
    WHEN stock_quantity <= 50 THEN '*'
    WHEN stock_quantity <= 51 THEN '**'
    ELSE '***' 
  END AS level 
FROM books;
```

## Exercises

```sql
SELECT 10 != 10 -- 0;

SELECT 15 > 14 && 99 - 5  <= 94; -- 1

SELECT 1 IN (5,3) || 9 BETWEEN 8 AND 10; -- 1

SELECT title FROM books WHERE released_year < 1980;

SELECT title,author_fname, author_lname FROM books WHERE author_fname IN ('Eggers', 'Carbon') || author_lname IN ('Eggers', 'Carver');

SELECT title, author_fname, author_lname FROM books 
WHERE author_lname LIKE 'C%' OR author_lname LIKE 'S%'; 

SELECT title, author_fname, author_lname FROM books 
WHERE author_lname LIKE 'C%' OR 'S%'; 


-- Desse jeito NÃO funciona, o próximo está correto. 
SELECT  title, author_lname,
  CASE 
    WHEN title IN ('stories') THEN 'Short stories'
    WHEN title IN ('Just kids') OR title IN ('A Heartbreaking Work') THEN 'Memoir'
    ELSE 'Novel'
  END AS TYPE
FROM books;


SELECT title, author_lname,
  CASE 
    WHEN title LIKE '%stories%' THEN 'Short stories'
    WHEN title LIKE '%Just kids%' OR title LIKE '%A Heartbreaking Work%' THEN 'Memoir'
    ELSE 'Novel'
  END AS TYPE
FROM books;


SELECT title, author_lname, 
  CONCAT(COUNT(*), ' ',
    CASE
      WHEN COUNT(*) = 1 THEN 'book'
      ELSE 'books'
    END   
  ) AS 'number'  
FROM books 
GROUP BY author_lname, author_fname;

```
