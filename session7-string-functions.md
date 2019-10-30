## Working with sql files

>mysql-ctl cli
source books.sql;

```
CREATE DATABASE book_shop;
USE book_shop;
database SELECT();
```

```
CREATE TABLE books 
	(
		book_id INT NOT NULL AUTO_INCREMENT,
		title VARCHAR(100),
		author_fname VARCHAR(100),
		author_lname VARCHAR(100),
		released_year INT,
		stock_quantity INT,
		pages INT,
		PRIMARY KEY(book_id)
	);

INSERT INTO books (title, author_fname, author_lname, released_year, stock_quantity, pages)
VALUES
('The Namesake', 'Jhumpa', 'Lahiri', 2003, 32, 291),
('Norse Mythology', 'Neil', 'Gaiman',2016, 43, 304),
('American Gods', 'Neil', 'Gaiman', 2001, 12, 465),
('Interpreter of Maladies', 'Jhumpa', 'Lahiri', 1996, 97, 198),
('A Hologram for the King: A Novel', 'Dave', 'Eggers', 2012, 154, 352),
('The Circle', 'Dave', 'Eggers', 2013, 26, 504),
('The Amazing Adventures of Kavalier & Clay', 'Michael', 'Chabon', 2000, 68, 634),
('Just Kids', 'Patti', 'Smith', 2010, 55, 304),
('A Heartbreaking Work of Staggering Genius', 'Dave', 'Eggers', 2001, 104, 437),
('Coraline', 'Neil', 'Gaiman', 2003, 100, 208),
('What We Talk About When We Talk About Love: Stories', 'Raymond', 'Carver', 1981, 23, 176),
("Where I'm Calling From: Selected Stories", 'Raymond', 'Carver', 1989, 12, 526),
('White Noise', 'Don', 'DeLillo', 1985, 49, 320),
('Cannery Row', 'John', 'Steinbeck', 1945, 95, 181),
('Oblivion: Stories', 'David', 'Foster Wallace', 2004, 172, 329),
('Consider the Lobster', 'David', 'Foster Wallace', 2005, 92, 343);
```

## Concat

```
SELECT CONCAT(author_fname, " ", author_lname) AS 'full name' FROM books;
```

```
SELECT author_fname AS first, author_lname AS last, 
CONCAT(author_fname, " ", author_lname) AS full
FROM books;
```

## Concat with the same symbol

```
SELECT CONCAT_WS(' - ', title, author_fname, author_lname)
FROM books;
```

## Substring
<p>The first letter is 1, NOT ZERO</p>
```
SELECT SUBSTRING('Hello World', 1, 4)
```

```
SELECT SUBSTRING('Hello World', -3) = RLD
```

```
SELECT CONCAT(SUBSTRING(title, 1, 10), '...') AS 'Short title' FROM books;
```

## Replace

```
SELECT REPLACE('Hello World', 'Hell', '@$¨!')
```

```
SELECT REPLACE(title, 'e', '3') AS replaced FROM books;
```

## Reverse

```
SELECT REVERSE('Hello world');
```

## Char length

```
SELECT CHAR_LENGTH('Hello Worlds ahsdi uahsiu hasidhud')
```

## Change String's case

```
SELECT UPPER('Hello Word');
SELECT LOWER('Hello Word');

```

## Exercise

```
SELECT REVERSE(UPPER('Why does my cat look at me with such hatred? well, thats not my cat, i dont have a cat '));

SELECT REPLACE(title, ' ', '->') AS title FROM books;

SELECT UPPER(CONCAT(author_fname, ' ',author_lname)) AS 'full name in caps' FROM books;

SELECT title, CHAR_LENGTH(title) AS LENGTH FROM books;

SELECT CONCAT(SUBSTRING(title, 1, 10), '...') AS 'short title',
        CONCAT(author_fname, ',', author_lname) AS author,
        CONCAT(stock_quantity, ' in stock') AS quantity
        FROM books;
 
```

