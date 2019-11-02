## Count

```sql
  SELECT COUNT(*) FROM books;
  
  SELECT COUNT(author_fname) FROM books;
  
  SELECT COUNT(DISTINCT author_fname) FROM books;
  
  SELECT COUNT(DISTINCT author_fname, author_lname) FROM books;
  
  SELECT COUNT(*) FROM books WHERE title LIKE '%the%';
  
```

## GROUP BY
 
```sql
  SELECT author_lname, COUNT(*) FROM books GROUP BY author_lname;
  
  SELECT author_fname, author_lname, COUNT(*) FROM books GROUP BY author_fname, author_lname;
  
```

## Min and Max

```sql
  SELECT Min(released_year) FROM books;
  
  SELECT Max(released_year) FROM books;
  
  ```
  
  ## SUBQUERIES - A problem with MIN and MAX
  
  <p>The query from the right runs first, returns a number of pages and  </p>
  
  - This causes problems with performance
  
  ```sql
    SELECT * FROM books WHERE pages = (SELECT Min(pages) FROM books);
    SELECT * FROM books WHERE pages = (SELECT Max(pages) FROM books);
  ```
  
  ## GROUP BY and Min/Max
  
  ```sql
    SELECT author_fname, author_lname, Min(released_year) FROM books GROUP BY author_fname, author_lname;
    SELECT author_fname, author_lname, Max(pages) FROM books GROUP BY author_fname, author_lname;
    SELECT CONCAT(author_fname, ' ', author_lname) AS author, MIN(released_year) FROM books GROUP BY author_lname, author_fname;
  ```
  
  ## Sum
  
  ```sql
    SELECT Sum(pages) FROM books;
    
    SELECT CONCAT(author_fname, ' ', author_lname) AS author, Sum(pages) FROM books GROUP BY author_lname, fname;
  ```
  
  ## Avg(average)
  
  - Sum things together and divide by the number of items
  - Decimal value
  
  ```sql
    SELECT AVG(released_year) FROM books;
    
    SELECT AVG(stock_quantity) FROM books GROUP BY released_year;
    
    SELECT CONCAT(author_fname, ' ', author_lname) AS author, Sum(pages) FROM books GROUP BY author_lname, fname;
  ```

## Exercise 

```sql
  SELECT CONCAT(author_fname, ' ', author_lname) AS author, pages FROM books WHERE pages = (SELECT Max(pages) FROM books);
  
  SELECT released_year AS year, Count(*) AS '#  Books', AVG(pages) AS 'avg pages' FROM books GROUP BY released_year;
  
```
