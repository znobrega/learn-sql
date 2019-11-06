# Relatiom MANY:MANY


```sql
CREATE TABLE series(
  id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
  title VARCHAR(150) NOT NULL,
  released_year YEAR(4) NOT NULL,
  genre VARCHAR(50) NOT NULL
);

CREATE TABLE reviewers(
  id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
  first_name VARCHAR(100) NOT NULL,
  last_name VARCHAR(100) NOT NULL
);

CREATE TABLE reviews(
  id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
  rating DECIMAL(5,2) NOT NULL,
  series_id INT,
  FOREIGN KEY(series_id) REFERENCES series(id),
  reviewer_id INT,
  FOREIGN KEY(reviewer_id) REFERENCES reviewers(id)
);


```
## Challenges
```sql
SELECT title, rating FROM series
INNER JOIN reviews 
  ON series.id = reviews.series_id;

SELECT title, AVG(rating) AS avg_rating 
FROM series
INNER JOIN reviews 
  ON series.id = reviews.series_id
GROUP BY series.id
ORDER BY AVG(rating);

SELECT first_name, last_name, rating FROM reviewers
INNER JOIN reviews
  ON reviewers.id = reviews.reviewer_id;

SELECT 
title
FROM series
LEFT JOIN reviews
  ON series.id = reviews.series_id
WHERE rating IS NULL;

SELECT 
  genre,
  AVG(rating) AS 'avg_rating'
FROM series
INNER JOIN reviews
  ON series.id = reviews.series_id
GROUP BY genre;

SELECT 
  first_name,
  last_name,
  COUNT(rating) AS 'COUNT',
  IFNULL(MIN(rating), 0) AS 'MIN',
  IFNULL(MAX(rating), 0) AS 'MAX',
  IFNULL(AVG(rating), 0) AS 'AVG',
  CASE 
    WHEN rating>=0 THEN 'ACTIVE'
    ELSE 'INACTIVE'
  END AS status
FROM reviewers
LEFT JOIN reviews
  ON reviewers.id = reviews.reviewer_id
GROUP BY last_name, first_name
ORDER BY status;

-- Double JOIN'S
SELECT 
  title, 
  rating, 
  CONCAT(first_name,' ', last_name) AS reviewer
FROM reviewers
INNER JOIN reviews
  ON reviewers.id = reviews.reviewer_id
INNER JOIN series
  ON reviews.series_id = series.id
ORDER BY title;
```