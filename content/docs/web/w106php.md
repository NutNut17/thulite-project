---
title: "PHP"
description: ""
summary: ""
date: 2024-10-20T01:13:16+08:00
lastmod: 2024-10-20T01:13:16+08:00
draft: false
weight: 106
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

#### Basic Syntax

{{< inline-svg src="svgs/logos/php.svg" width="100px" height="79px" class="svg-inline-custom" >}}

```php
<!DOCTYPE html>
<html>
<head>
  <title>PHP Intro</title>
</head>
<body>
  <h1>Welcome to PHP</h1>

  <?php
    function calc($x, $y) {
      if ($x > $y)
        for ($i = 1; $i <= 5; $i++) {
          echo "Hi";
        }
    }

    $x = 1;
    $y = 0;

    calc($x, $y);
  ?>
</body>
</html>
```

#### Forms

```html
<form method="POST" action="process.php">
  <input type="text" name="username" placeholder="Enter your name">
  <input type="submit" value="Submit">
</form>
```

```php {title="process.php"}
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
  $username = $_POST['username'];  // Get form data
  echo "Hello, $username!";
}
?>
```

#### MySQL

```php
<?php
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "test_db";

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
  die("Connection failed: " . $conn->connect_error);
}

// Query data
$sql = "SELECT id, name FROM users";
$result = $conn->query($sql);

if ($result->num_rows > 0) {
  while($row = $result->fetch_assoc()) {
    echo "ID: " . $row["id"]. " - Name: " . $row["name"]. "<br>";
  }
} else {
  echo "0 results";
}

$conn->close();
?>
```
