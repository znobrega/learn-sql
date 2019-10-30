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
