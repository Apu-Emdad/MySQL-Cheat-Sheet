## Connection

```php
<?php
$servername = "localhost";
$username = "root"; // Default username
$password = "";     // Default password
$dbname = "your_database";

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully";
?>

```

## Show Databases

```php
$sql = "SHOW DATABASES";
$result = $conn->query($sql);
```

## Create Database

```php
$sql = "CREATE DATABASE acme";
$result = $conn->query($sql);
```

## Delete Database

```php
$sql = "DROP DATABASE acme";
$result = $conn->query($sql);
```

## Select Database

```php
$sql = "USE acme";
$result = $conn->query($sql);
```

## Create Table

```php
$sql = "CREATE TABLE users(
    id INT AUTO_INCREMENT,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    email VARCHAR(50),
    password VARCHAR(20),
    location VARCHAR(100),
    dept VARCHAR(100),
    is_admin TINYINT(1),
    register_date DATETIME,
    PRIMARY KEY(id)
)";
$result = $conn->query($sql);

```

## Delete / Drop Table

```php
$sql = "DROP TABLE tablename";
$result = $conn->query($sql);

```

## Show Tables

```php
$sql = "SHOW TABLES";
$result = $conn->query($sql);
```

## Select

```php
$sql = "SELECT * FROM users";
$result = $conn->query($sql);

$sql = "SELECT first_name, last_name FROM users";
$result = $conn->query($sql);
```

## Where Clause

```php
$sql = "SELECT * FROM users WHERE location='Massachusetts'";
$result = $conn->query($sql);

$sql = "SELECT * FROM users WHERE location='Massachusetts' AND dept='sales'";
$result = $conn->query($sql);

$sql = "SELECT * FROM users WHERE is_admin = 1";
$result = $conn->query($sql);

$sql = "SELECT * FROM users WHERE is_admin > 0";
$result = $conn->query($sql);

```

## Delete Row

```php
$sql = "DELETE FROM users WHERE id = 6";
$result = $conn->query($sql);
```

## Update Row

```php
$sql = "UPDATE users SET email = 'freddy@gmail.com' WHERE id = 2";
$result = $conn->query($sql);
```

## Add New Column

```php
$sql = "ALTER TABLE users ADD age VARCHAR(3)";
$result = $conn->query($sql);
```

## Modify Column

```php
$sql = "ALTER TABLE users MODIFY COLUMN age INT(3)";
$result = $conn->query($sql);

```

## Order By (Sort)

```php
$sql = "SELECT * FROM users ORDER BY last_name ASC";
$result = $conn->query($sql);

$sql = "SELECT * FROM users ORDER BY last_name DESC";
$result = $conn->query($sql);
```

## Concatenate Columns

```php
$sql = "SELECT CONCAT(first_name, ' ', last_name) AS 'Name', dept FROM users";
$result = $conn->query($sql);
```

## Select Distinct Rows

```php
$sql = "SELECT DISTINCT location FROM users";
$result = $conn->query($sql);
```

## Between (Select Range)

```php
$sql = "SELECT * FROM users WHERE age BETWEEN 20 AND 25";
$result = $conn->query($sql);
```

## Like (Searching)

```php
$sql = "SELECT * FROM users WHERE dept LIKE 'd%'";
$result = $conn->query($sql);

$sql = "SELECT * FROM users WHERE dept LIKE 'dev%'";
$result = $conn->query($sql);

$sql = "SELECT * FROM users WHERE dept LIKE '%t'";
$result = $conn->query($sql);

$sql = "SELECT * FROM users WHERE dept LIKE '%e%'";
$result = $conn->query($sql);

```

## Not Like

```php
$sql = "SELECT * FROM users WHERE dept NOT LIKE 'd%'";
$result = $conn->query($sql);
```

## IN

```php
$sql = "SELECT * FROM users WHERE dept IN ('design', 'sales')";
$result = $conn->query($sql);
```

## Create & Remove Index

```php
$sql = "CREATE INDEX LIndex On users(location)";
$result = $conn->query($sql);

$sql = "DROP INDEX LIndex ON users";
$result = $conn->query($sql);
```

## New Table With Foreign Key (Posts)

```php
$sql = "CREATE TABLE posts(
    id INT AUTO_INCREMENT,
    user_id INT,
    title VARCHAR(100),
    body TEXT,
    publish_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY(id),
    FOREIGN KEY (user_id) REFERENCES users(id)
)";
$result = $conn->query($sql);
```

## Add Data to Posts Table

```php
$sql = "INSERT INTO posts(user_id, title, body) VALUES
(1, 'Post One', 'This is post one'),
(3, 'Post Two', 'This is post two'),
(1, 'Post Three', 'This is post three'),
(2, 'Post Four', 'This is post four'),
(5, 'Post Five', 'This is post five'),
(4, 'Post Six', 'This is post six'),
(2, 'Post Seven', 'This is post seven'),
(1, 'Post Eight', 'This is post eight'),
(3, 'Post Nine', 'This is post none'),
(4, 'Post Ten', 'This is post ten')";

$result = $conn->query($sql);
```

## INNER JOIN

```php
$sql = "SELECT
  users.first_name,
  users.last_name,
  posts.title,
  posts.publish_date
FROM users
INNER JOIN posts
ON users.id = posts.user_id
ORDER BY posts.title";

$result = $conn->query($sql);
```

## New Table With 2 Foriegn Keys

```php
$sql = "CREATE TABLE comments(
    id INT AUTO_INCREMENT,
    post_id INT,
    user_id INT,
    body TEXT,
    publish_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY(id),
    FOREIGN KEY(user_id) references users(id),
    FOREIGN KEY(post_id) references posts(id)
)";

$result = $conn->query($sql);
```

## Add Data to Comments Table

```php
$sql = "INSERT INTO comments(post_id, user_id, body) VALUES
(1, 3, 'This is comment one'),
(2, 1, 'This is comment two'),
(5, 3, 'This is comment three'),
(2, 4, 'This is comment four'),
(1, 2, 'This is comment five'),
(3, 1, 'This is comment six'),
(3, 2, 'This is comment six'),
(5, 4, 'This is comment seven'),
(2, 3, 'This is comment seven')";

$result = $conn->query($sql);
```

## Left Join

```php
$sql = "SELECT
comments.body,
posts.title
FROM comments
LEFT JOIN posts ON posts.id = comments.post_id
ORDER BY posts.title";

$result = $conn->query($sql);
```

## Join Multiple Tables

```php
$sql = "SELECT
comments.body,
posts.title,
users.first_name,
users.last_name
FROM comments
INNER JOIN posts on posts.id = comments.post_id
INNER JOIN users on users.id = comments.user_id
ORDER BY posts.title";

$result = $conn->query($sql);
```

## Aggregate Functions

```php
$sql = "SELECT COUNT(id) FROM users";
$result = $conn->query($sql);

$sql = "SELECT MAX(age) FROM users";
$result = $conn->query($sql);

$sql = "SELECT MIN(age) FROM users";
$result = $conn->query($sql);

$sql = "SELECT SUM(age) FROM users";
$result = $conn->query($sql);

$sql = "SELECT UCASE(first_name), LCASE(last_name) FROM users";
$result = $conn->query($sql);
```

## Group By

```php
$sql = "SELECT age, COUNT(age) FROM users GROUP BY age";
$result = $conn->query($sql);

$sql = "SELECT age, COUNT(age) FROM users WHERE age > 20 GROUP BY age";
$result = $conn->query($sql);

$sql = "SELECT age, COUNT(age) FROM users GROUP BY age HAVING count(age) >= 2";
$result = $conn->query($sql);
```
