```sql
DROP DATABASE ig_clone;
CREATE DATABASE ig_clone;
USE ig_clone;

CREATE TABLE users(
  id INT PRIMARY KEY AUTO_INCREMENT,
  username VARCHAR(255) UNIQUE NOT NULL,
  created_at TIMESTAMP DEFAULT NOW()  
);

CREATE TABLE photos(
  id INT PRIMARY KEY AUTO_INCREMENT,
  image_url VARCHAR(255) NOT NULL,
  user_id INT NOT NULL,
  created_at TIMESTAMP DEFAULT NOW(),
  FOREIGN KEY(user_id) 
    REFERENCES users(id)
    ON DELETE CASCADE
);

CREATE TABLE comments(
  id INT PRIMARY KEY AUTO_INCREMENT,
  comment_text VARCHAR(255) NOT NULL,
  user_id INT NOT NULL,
  photo_id INT NOT NULL,
  created_at TIMESTAMP DEFAULT NOW(),
  FOREIGN KEY(user_id) 
    REFERENCES users(id)
    ON DELETE CASCADE,
  FOREIGN KEY(photo_id)
    REFERENCES photos(id)
    ON DELETE CASCADE
);

-- We dont reference likes, so don't need a ID
CREATE TABLE likes(
  user_id INT NOT NULL,
  photo_id INT NOT NULL,
  created_at TIMESTAMP DEFAULT NOW(),
  FOREIGN KEY(user_id) 
    REFERENCES users(id)
    ON DELETE CASCADE,
  FOREIGN KEY(photo_id)
    REFERENCES photos(id)
    ON DELETE CASCADE,
  PRIMARY KEY(user_id, photo_id) -- this combination can't repeat, so it's unique
);

CREATE TABLE follows(
  follower_id INT NOT NULL,
  followee_id INT NOT NULL,
  created_at TIMESTAMP DEFAULT NOW(),
  FOREIGN KEY(follower_id) REFERENCES users(id) ON DELETE CASCADE,
  FOREIGN KEY(followee_id) REFERENCES users(id) ON DELETE CASCADE,
  PRIMARY KEY(follower_id, followee_id)
);

CREATE TABLE tags(
  id INT PRIMARY KEY AUTO_INCREMENT,
  tag_name VARCHAR(255) UNIQUE,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE photo_tags(
  photo_id INT NOT NULL,
  tag_id INT NOT NULL,
  FOREIGN KEY(photo_id) 
    REFERENCES photos(id)
    ON DELETE CASCADE,
  FOREIGN KEY(tag_id)
    REFERENCES users(id)
    ON DELETE CASCADE,
  PRIMARY KEY(photo_id, tag_id)
);

```

### Challenge 1
```sql
SELECT username, created_at FROM users
ORDER BY created_at
LIMIT 5;
```

### Challenge 2
```sql
SELECT DAYNAME(created_at) AS day, COUNT(*) AS register_count FROM users
GROUP BY day
ORDER BY register_count DESC
LIMIT 2;
```

### Challenge 3
```sql
SELECT username FROM users
LEFT JOIN photos
  ON users.id = photos.user_id
WHERE photos.image_url IS NULL;
```

### Challenge 4
```sql
SELECT  
  username,
  image_url,
  photos.id,
  COUNT(*) AS total 
FROM users
INNER JOIN photos
  ON photos.user_id = users.id
INNER JOIN likes
  ON photos.id = likes.photo_id
GROUP BY likes.photo_id
ORDER BY total DESC
LIMIT 1;

SELECT 
  username,
  photos.id,
  photos.image_url,
  COUNT(*) AS total
FROM photos
INNER JOIN likes
  ON likes.photo_id = photos.id
INNER JOIN users
  ON users.id = photos.user_id
GROUP BY photos.id
ORDER BY total DESC
LIMIT 1;

```

### Challenge 5
```sql
SELECT (SELECT COUNT(*) FROM photos)/(SELECT COUNT(*) FROM users) AS avg_posts;

SELECT COUNT(*)/(SELECT COUNT(*) FROM users) FROM photos;


```

### Challenge 6
```sql

SELECT 
  tag_name,
  COUNT(*) AS total
FROM photo_tags
INNER JOIN tags
  ON tags.id = photo_tags.tag_id 
GROUP BY tag_id
ORDER BY total DESC
LIMIT 5;
```

### Challenge 6
```sql
SELECT * FROM photos;

SELECT 
  username,
  CASE 
    WHEN COUNT(user_id)=(SELECT COUNT(*) FROM photos) THEN user_id
  END AS THEBOT
FROM likes
INNER JOIN users
  ON likes.user_id = users.id
GROUP BY user_id;
--HAVING THEBOT = (SELECT COUNT(*) FROM photos);

SELECT 
  username,
  COUNT(*) AS total_likes
FROM users
INNER JOIN likes
  ON users.id = likes.user_id
GROUP BY likes.user_id
HAVING total_likes = (SELECT COUNT(*) FROM photos);
-- Having se aplica ao grupo
-- WHERE se aplica em linhas individuais
```