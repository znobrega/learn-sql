# SQL

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
)
```


## DEFAULT VALUE 
<p>You can specify a default value that will furfill the table when you dont provide a value</p>

´´´
CREATE TABLE cats3(
  name VARCHAR(100) DEFAULT 'unnamed',
  age INT DEFAULT 99
)
´´´

## NOT NULL and DEFAULT

<p>Use NOT NULL and DEFAULT is redundant?</p>
<p>NO, beacause you can put a NULL value manually. If you try to insert a NULL value with NOT NULL, a error will appears</p>

´´´
CREATE TABLE cats4(
  name VARCHAR(30) NOT NULL DEFAULT 'no name provided',
  age INT NOT NULL DEFAULT 99
)

´´´

## PRIMARY KEY
<p>Unique ID</p>

´´´
CREATE TABLE unique_cats(
  cat_id INT NOT NULL AUTO_INCREMENT,
  name NOT NULL DEFAULT 'unnamed',
  age INT NOT NULL DEFAULT 99,
  PRIMARY KEY (cat_id)
);
´´´

## Exercice session 4

´´´
CREATE TABLE employees(
	id INT NOT NULL AUTO_INCREMENT,
	last_name VARCHAR(40) NOT NULL, 
	first_name VARCHAR(40) NOT NULL,
	middle_name VARCHAR(40),
	age INT NOT NULL DEFAULT 99,
	current_status VARCHAR(60) NOT NULL DEFAULT 'employed',
	PRIMARY KEY(id)
);
´´´

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


