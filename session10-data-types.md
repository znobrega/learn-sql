```sh
$ cd dillinger
$ npm install -d
$ node app
```

Session 10 - Types and 

# Text
 ----------------

 - **CHAR**: is faster for fixed length text

     > State abreviation, sex, flags

 when you have a char(10) and gives a string with length 4, the value is right-padded with spaces to complete the specified length. when you take the value, the spaces are removed

- **VARCHAR**: Use this

| Values    | CHAR(4)   | Storage  | VARCHAR(4)   | Storage  |
| --------- |:---------:| :-------:|:------:|------:|
| ''        | '`____`'  | 4 bytes | ''       | 1 bytes
| 'ab'      | 'ab`__`'  | 4 bytes | 'ab'     | 3 bytes
| 'abcd'    | 'abcd'    | 4 bytes | 'abcd'   | 5 bytes
| 'abcdefg' | 'abcdefg' | 4 bytes | 'abcdefg'| 5 bytes
 
 
 # Number
 ----------------
 #### Decimal
Decimal(**M**, **D**)

 - M: number of digits, 1~65
 - D: number of digits after the comma, 0~30. can't be larger than M
 
    > Decimal(5, 2): 999.99

 1 - If the given number is larger than the maximun number allowed, this number will be the maximum number allowesd
 2 - If has more decimal digites, the number will be rounded up
 3 - Fixed point with exact calculations
 
 #### Float and Double
> Double is better, is bigger but more precise

 1 - Store larger number with less space, but it come at the cost of precision
 
 | Data Type    | Memory needed  | Precision issues  | 
| --------- |:---------:| :-------:|
| FLOAT     |  4 bytes  | ~7 DIGITS | 
| DOUBLE    |  8 bytes  | ~15 DIGITS |

> the precision is a real problem.
8877665544.45 is storage as 8877670000 

    Decimal > Double > Float
    
# Date
 ----------------
 #### DATE
'YYYY-MM-DD'
date but no time

#### TIME
time but no date
'HH:MM:SS'

#### DATETIME
'YYYY-MM-DD HH:MM:SS'

#### Functions

> CURDATE() - CURRENT DATE
CURTIME() - CURRENT TIME
NOW() - CURRENT DATE TIME

```sql 
INSERT INTO people(name birthdate, bithtime, bithdatetime) VALUES('illson', CURDATE(), CURTIME(), NOW());
```

> DAY() Number 1~31
DAYNAME() Sunday~Saturday
DAYOFWEEK() Number: 1~7 
DAYOFYEAR() Number: 1~365...
HOUR()
MINUTE()
SECOND()

```
SELECT DAY(birtdatetime) FROM people;
```

> MONTH() Number: 1~12
MONTHNAME() January~December

the function to work with date is: **DATE-FORMAT()**
[Format date docs](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-format)

```sql
mysql> SELECT DATE_FORMAT('2009-10-04 22:23:00', '%W %M %Y');
        -> 'Sunday October 2009'
mysql> SELECT DATE_FORMAT('2007-10-04 22:23:00', '%H:%i:%s');
        -> '22:23:00'
mysql> SELECT DATE_FORMAT('1900-10-04 22:23:00',
    ->                 '%D %y %a %d %m %b %j');
        -> '4th 00 Thu 04 10 Oct 277'
mysql> SELECT DATE_FORMAT('1997-10-04 22:23:00',
    ->                 '%H %k %I %r %T %S %w');
        -> '22 22 10 10:23:00 PM 22:23:00 00 6'
mysql> SELECT DATE_FORMAT('1999-01-01', '%X %V');
        -> '1998 52'
mysql> SELECT DATE_FORMAT('2006-06-00', '%d');
        -> '00'
````

## Math date

#### DATEDIFF(expr1, expre2)
Subtract the first argument by the second
gives the result in DAYS
```sql
SELECT DATEDIFF(NOW(), birthdate) FROM people 
```

#### DATE_ADD(date, INTERVAL expr_unit) anad DATE_SUB(date, INTERVAL expr_unit)
#### +/-

```sql
  SELECT DATE_ADD('2100-12-31 23:59:59', INTERVAL 1 SECOND);
  SELECT DATE_ADD('2100-12-31 23:59:59', INTERVAL 1 DAY);
  SELECT DATE_ADD('2100-12-31 23:59:59', INTERVAL 1 DAY_SECOND);
```

```sql
SELECT '2100-12-31 23:59:59' +INTERVAL 1 DAY FROM people;
SELECT '2100-12-31 23:59:59' +INTERVAL 1 DAY + INTERVAL 10 MONTH + INTERVAL 13 HOUR FROM books;
```

#### Timestamp 
```sql
CREATE TABLE comments(
    content VARCHAR(200),
    created_at TIMESTAMP DEFAULT NOW()
    updated_at TIMESTAMP DEAFAULT NOW() ON UPDATE NOW()
);

can use CURRENT_TIMESTAMP instead of NOW()

