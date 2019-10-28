# SQL
https://ide-run.goorm.io
>mysql-ctl cli
>source file.sql;

## Capitalize commands just to diffentiate what comes from sql and what is a custom name   
## All commands:   
```
SHOW DATABASES;

CREATE DATABASE hello_word;
CREATE DATABASE soap_store;

DROP DATABASE hello_world;

USE soap_store;
SELECT database(); // Tells the current database

CREATE TABLE tablename(
  column_name data_type,
  column_name data_type,  
);

SHOW TABLES;

SHOW COLUMNS FROM <tablename>;
or 
DESC <tablename>;

DROP TABBLE <tablename> 

INSERTO INTO  <tablename>(<column>, <column>) VALUES ("Jetson", 6);
INSERTO INTO  cats(name, age) VALUES ("Jetson", 6);

SELECT * FROM cats;

INSERTO INTO  cats(name, age) 
VALUES ("Jetson", 6),
       ("Happy", 2),
       ("lotsofcat", 5);
       
SHOW WARNINGS;

CREATE TABLE cats2(
  name VARCHAR(30) NOT NULL,
  age INT NOT NULL,
)

=================== NEW TABLE CATS =======================
CREATE TABLE cats(
	cat_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
	name VARCHAR(100),
	breed VARCHAR(100),
	age INT
);

INSERT INTO cats(name, breed, age)
VALUES ('Ringo', 'Tabby', 4),
	('Cindy', 'Maine Coon', 10),
	('Dumbledore', 'Maine Coon', 11),
	('Egg', 'Persian', 4),
	('Misty', 'Tabby', 13),
	('Gerorge Michael', 'Ragdoll', 9),
	('Jackson', 'Sphynx', 7)
);

SELECT cat_id, age FROM cats WHERE age = cat_id;
```

## Tables - The true heart of SQL  

<img src="https://upload.wikimedia.org/wikipedia/commons/9/95/Metamodel_of_Facebook.jpg" alt="Facebook models, its not complete"/>

## Data types

Numeric | String | Date
------------------------
INT | VARCHAR(1,255) | DATE

Tweet
username = VARCHAR(15)
content = VARCHAR(140)
likes = INT

```
CREATE TABLE tablename(
  username VARCHAR(15),
  content VARCHAR(140),
  likes INT
);

```

Pastries table
```

CREATE TABLE pastries(
  name VARCHAR(50),
  quantity INT
);

INSERT INTO pastries(name, quantity)
VALUES("john", 40), ("alves", 3), ("teal", 1);

```

## NULL or NOT_NULL
<p> Sql has a field NULL that allows or not a row value to be null. If you don't provide a value the sql will insert NULL values</p>
<p>When you are creating a TABLE, you can specify NOT NULL</p>

```
CREATE TABLE cats2(
  name VARCHAR(30) NOT NULL,
  age INT NOT NULL,
```


## DEFAULT VALUE 
<p>You can specify a default value that will furfill the table when you dont provide a value</p>

```
CREATE TABLE cats3(
  name VARCHAR(100) DEFAULT 'unnamed',
  age INT DEFAULT 99
)
```

## NOT NULL and DEFAULT

<p>Use NOT NULL and DEFAULT is redundant?</p>
<p>NO, beacause you can put a NULL value manually. If you try to insert a NULL value with NOT NULL, a error will appears</p>

```
CREATE TABLE cats4(
  name VARCHAR(30) NOT NULL DEFAULT 'no name provided',
  age INT NOT NULL DEFAULT 99
)
```

## PRIMARY KEY
<p>Unique ID</p>

```
CREATE TABLE unique_cats(
  cat_id INT NOT NULL AUTO_INCREMENT,
  name NOT NULL DEFAULT 'unnamed',
  age INT NOT NULL DEFAULT 99,
  PRIMARY KEY (cat_id)
);
```

## Exercice session 4

```
CREATE TABLE employees(
	id INT NOT NULL AUTO_INCREMENT,
	last_name VARCHAR(40) NOT NULL, 
	first_name VARCHAR(40) NOT NULL,
	middle_name VARCHAR(40),
	age INT NOT NULL DEFAULT 99,
	current_status VARCHAR(60) NOT NULL DEFAULT 'employed',
	PRIMARY KEY(id)
);
```

or 

´´´
CREATE TABLE employees2(
	id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  first_name VARCHAR(40) NOT NULL,
	last_name VARCHAR(40) NOT NULL, 
	middle_name VARCHAR(40),
	age INT NOT NULL DEFAULT 99,
	current_status VARCHAR(60) NOT NULL DEFAULT 'employed'
);

INSERT INTO employees2(first_name, last_name, age)
VALUES('Carlos', 'Nobrega', 19);

SELECT * FROM employees2;
´´´

## Restarting the cat table

```
DROP TABLE cats;
CREATE TABLE cats(
	cat_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
	name VARCHAR(100),
	breed VARCHAR(100),
	age INT
);

INSERT INTO cats(name, breed, age)
VALUES ('Ringo', 'Tabby', 4),
	('Cindy', 'Maine Coon', 10),
	('Dumbledore', 'Maine Coon', 11),
	('Egg', 'Persian', 4),
	('Misty', 'Tabby', 13),
	('Gerorge Michael', 'Ragdoll', 9),
	('Jackson', 'Sphynx', 7)
);
```

# CRUD
C | CREATE
----------
R | READ
U | UPDATE
D | DELETE

## READ

```
SELECT name, age FROM cats;
```

<p>WHERE will appears everyWHERE</p>
SELECT * FROM cats WHERE breed='Tabby';

```
SELECT name, breed FROM cats;
```

```
SELECT name, age FROM cats WHERE breed='Tabby' ;
```

```
SELECT cat_id, age FROM cats WHERE age <= 7;
```

<p>Comparation is different from PL's</p>
```
SELECT cat_id, age FROM cats WHERE age = cat_id;
```

## Alias
<p>You can give a NICK to the field when it prints </p>
```
SELECT cat_id AS id, name FROM cats;
```

## UPDATE
<p>All breed's cats with breed='Tabby' will be changed to 'Shorthair</p>
```
UPDATE cats SET breed='Shorthair'
WHERE breed='Tabby'
```

<p>Make sure you targgeting the right data</p>

```
UPDATE cats SET age=14
WHERE name='Misty';
```

```
UPDATE cats SET name='Jack'
WHERE name='Jackson';
```

```
UPDATE cats SET breed='British Shorthair'
WHERE name="Ringo";
```

```
UPDATE cats SET age=12
WHERE breed='Maine Coon';
```

## DELETE 

<p>Very similar to UPDATE</p>

```
DELETE FROM cats WHERE name='Egg';
```

<p>Be carefull, this command deletes all data</p>
```
DELETE FROM cats;
```

## Complete CRUD
<p>CREATE</p>
```
CREATE TABLE shirts(
	shirt_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
	article VARCHAR(20) NOT NULL,
	color VARCHAR(30) NOT NULL,
	shirt_size(3) NOT NULL,
	last_worn INT NOT NULL
);

INSERT INTO cats(article, color, shirt_size, last_worn)
VALUES ('t-shirt', 'white', 'S', 10),
	('t-shirt', 'green', 'S', 200),
	('polo shirt', 'black', 'M', 10),
	('tank top', 'blue', 'S', 50),
	('t-shirt', 'pink', 'S', 0),
	('polo shirt', 'red', 'M', 5),
	('tank top', 'white', 'S', 200),
	('tank top', 'blue', 'M', 15);
	
INSERT INTO shirts(article, color, shirt_size, last_won)
VALUES ('polo', 'Purple', 'M', 50);


```

<p>READ</p>
```
SELECT article, color FROM shirts;
SELECT * FROM shirts WHERE shirt_size='M';
SELECT article, color, shirt_size, last_worn FROM shirts WHERE shirt_size='M';
```

<p>UPDATE</p>
```
UPDATE shirts SET shirt_size='L'
WHERE article='polo shirt';
```

```
UPDATE shirts SET last_worn=0
WHERE last_worn=15;

```

```
UPDATE shirts SET shirt_size='XS', color='off white'
WHERE color='white';
```

<p>DELETE</p>
```
DELETE FROM shirts
WHERE last_worn >= 200;
```

```
DELETE FROM shirts
WHERE article='tank top';
```

```
DELETE FROM shirts;
DROP TABLE shirts;

show tables;

DESC shirts;
```

