>OBS: Those properties are applied at rows

## DISTINCT

<p>DISTINCT comes after SELECT</p>
<p>Remove the values duplicates</p>

```sql
  SELECT DISTINCT author_fname FROM books;
  
  SELECT DISTINCT released_year FROM books;
  
  SELECT DISTINCT CONCAT(author_fname, ' ', author_lname) FROM books;
```

<p>Applying DISTINCT in a row</p>

```sql
  SELECT DISTINCT author_fname, author_lname FROM books;
```

## ORDER BY // SORTING

<p>ASCENDING by default</p>
```sql 
  SELECT author_lname FROM books ORDER BY author_lname;
```

<p>DESCENDING/REVERSE</p>

```sql 
  SELECT author_lname FROM books ORDER BY author_lname DESC;
```

<p>SHORTCURT, the is refering to the the second element on the SELECT. In this case is refering to *author_fname*</p>

```sql 
  SELECT title, author_fname, author_lname FROM books ORDER BY 2;
```

<p>Also, you can ORDER BY two columns</p>
<p>First sort the first param, keeps the sort and sort again with the second param</p>

```sql
SELECT title, author_fname, author_lname FROM books ORDER BY author_fname, author_lname;
```

## LIMIT


```sql
  SELECT title, released_year FROM books ORDER BY 2 DESC LIMIT 10;
  OR
  SELECT title, released_year FROM books ORDER BY 2 DESC LIMIT 0,10;
```

<p>First param: Start Secon param: how many from the start</p>
```sql
  SELECT title, released_year FROM books ORDER BY 2 DESC LIMIT 3,10;
```

## LIKE
- Pattern matching
- Wildcard: % 
<p>%da% => anything: da :anything</p >

```sql
  SELECT * FROM books WHERE author_fname LIKE '%da%';
```

<p>da% => start with 'da' then :anything</p >

```sql
  SELECT * FROM books WHERE author_fname LIKE 'da%';
```

<p>Wildcard: _____(four underscore)</p>
- _ represents a character
- 4 underscores means that i want 4 DIGITS

```sql
  SELECT * FROM books WHERE stock_quantity LIKE '____';
```

- You can use underscore and mod to work with RegExp
- OBS: \% or \_=> match the symbol 


## Exercises

```sql
SELECT title FROM books WHERE title LIKE '%stories%';

SELECT title, pages FROM books ORDER BY 2 DESC LIMIT 1;

SELECT CONCAT_WS(' - ', title, released_year) AS summary FROM books ORDER BY released_year DESC LIMIT 0,3; 

SELECT title, author_lname FROM books WHERE author_lname LIKE '% %';

SELECT title, author_lname FROM books ORDER BY author_lname, title;

SELECT CONCAT('MY FAVORITE AUTHOR IS ', author_fname, ' ', author_lname) AS yell FROM books ORDER BY author_lname;
```
