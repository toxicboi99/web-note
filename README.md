**PHP Notes**

## 1. Declaring a Class in PHP
### **Definition:**
A class is a blueprint for creating objects in PHP. It defines properties (variables) and methods (functions) that an object can have.

### **Key Concepts:**
- Classes encapsulate data and behavior.
- Objects are instances of a class.
- Methods are functions inside a class.

### **Types:**
- Concrete Class
- Abstract Class
- Final Class
- Trait
- Interface

### **Syntax:**
```php
class Car {
    public $brand; // Property
    
    public function setBrand($brand) {
        $this->brand = $brand;
    }
    
    public function getBrand() {
        return $this->brand;
    }
}
```

### **Example:**
```php
$myCar = new Car(); // Object creation
$myCar->setBrand("Toyota");
echo $myCar->getBrand();
```

## 2. Creating an Object, Accessing Properties and Methods
### **Definition:**
An object is an instance of a class. You can access properties and methods using the `->` operator.

### **Example:**
```php
class Student {
    public $name;
    
    public function setName($name) {
        $this->name = $name;
    }
    
    public function getName() {
        return $this->name;
    }
}

$student1 = new Student();
$student1->setName("John");
echo $student1->getName();
```

## 3. Understanding File & Directory
### **Definition:**
A file is a data storage medium, while a directory (or folder) is a container for files and other directories.

### **Key Concepts:**
- File handling includes reading, writing, and managing files.
- Directory handling includes creating, deleting, and listing directories.

## 4. File Functions in PHP
### **Common File Functions:**
- `fopen()`: Opens a file.
- `fwrite()`: Writes to a file.
- `fread()`: Reads a file.
- `fclose()`: Closes a file.
- `file_exists()`: Checks if a file exists.

### **Example:**
```php
$file = fopen("example.txt", "w");
fwrite($file, "Hello, PHP File Handling!");
fclose($file);
```

## 5. Working with Directories
### **Directory Functions:**
- `mkdir()`: Creates a directory.
- `rmdir()`: Removes a directory.
- `scandir()`: Lists files in a directory.

### **Example:**
```php
mkdir("new_folder"); // Creating a directory
```

## 6. Building a Text Editor
### **Components:**
- HTML form for text input
- PHP script for file handling

### **Example:**
```php
if(isset($_POST['save'])) {
    $file = fopen("notes.txt", "w");
    fwrite($file, $_POST['content']);
    fclose($file);
}
```

## 7. File Uploading & Downloading
### **File Uploading:**
- Use an HTML form with `enctype="multipart/form-data"`.
- Use `move_uploaded_file()` to store the uploaded file.

### **Example:**
```php
if(isset($_FILES["file"])) {
    move_uploaded_file($_FILES["file"]["tmp_name"], "uploads/" . $_FILES["file"]["name"]);
}
```

### **File Downloading:**
```php
header('Content-Type: application/octet-stream');
header('Content-Disposition: attachment; filename="example.txt"');
readfile("example.txt");
```

## **Advantages of PHP File Handling**
- Efficient data storage and retrieval.
- Automates file-based operations.
- Supports multiple file types.

## **Disadvantages of PHP File Handling**
- Security risks like unauthorized access.
- Can be slow for large-scale data operations.

## **Applications of PHP File Handling**
- Content Management Systems (CMS)
- Log file management
- User data storage

## **Important Notes:**
- Always validate and sanitize user input for file uploads.
- Set proper file permissions for security.
- Use `unlink()` to delete files when necessary.

**PHP Sessions, Cookies, and Database Operations**

## 1. **Starting & Destroying PHP Session**
### **Definition:**
A PHP session is a mechanism used to store user information across multiple pages. Unlike cookies, session data is stored on the server, making it more secure. Each user session is assigned a unique session ID, which is used to retrieve stored session data when the user navigates different pages.

### **Starting a Session:**
```php
session_start();
$_SESSION['username'] = 'JohnDoe';
echo "Session started";
```

### **Destroying a Session:**
```php
session_start();
session_destroy();
echo "Session destroyed";
```

---
## 2. **Turning on Auto Session**
### **Definition:**
Auto session starts automatically without explicitly calling `session_start()`. This helps in maintaining session state without requiring additional code in every script.

### **Enabling Auto Session in `php.ini`:**
Modify `php.ini` and set:
```ini
session.auto_start = 1
```
This automatically starts a session on every page load.

---
## 3. **Anatomy of a Cookie**
### **Definition:**
A cookie is a small piece of data stored in the user’s browser, used for tracking user activities, maintaining login sessions, and storing user preferences. Cookies are sent with every HTTP request to the server, making them useful for persistent data storage across sessions.

### **Components of a Cookie:**
- **Name:** Identifier for the cookie.
- **Value:** The actual data stored in the cookie.
- **Expiry time:** The duration before the cookie expires.
- **Path:** The scope of the cookie within the domain.
- **Domain:** Specifies which domain can access the cookie.
- **Secure flag:** Ensures the cookie is transmitted only over HTTPS.
- **HttpOnly flag:** Restricts access to the cookie via JavaScript, enhancing security.

---
## 4. **Setting, Accessing & Deleting Cookies with PHP**
### **Definition:**
Cookies allow websites to store user-related information persistently on the client-side. They help with personalization, user authentication, and tracking browsing behavior.

### **Setting a Cookie:**
```php
setcookie("username", "JohnDoe", time() + 3600, "/");
```

### **Accessing a Cookie:**
```php
echo $_COOKIE['username'];
```

### **Deleting a Cookie:**
```php
setcookie("username", "", time() - 3600, "/");
```

---
## 5. **Sessions Without Cookies**
### **Definition:**
Sessions can work without cookies by passing the session ID in the URL. This is useful when cookies are disabled on the client’s browser.

### **Using URL-Based Sessions:**
```php
session_start();
echo "<a href='nextpage.php?".session_name()."=".session_id()."'>Next Page</a>";
```

---
## 6. **Connection with MySQL Database**
### **Definition:**
Connecting PHP with MySQL allows dynamic interaction with databases, enabling data storage, retrieval, and manipulation in web applications. The `mysqli` and `PDO` extensions are commonly used for database connectivity.

### **Establishing a Database Connection:**
```php
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "my_database";

$conn = new mysqli($servername, $username, $password, $dbname);
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully";
```

---
## 7. **CRUD Operations in PHP with MySQL**
### **Definition:**
CRUD stands for Create, Read, Update, and Delete – the four fundamental operations for managing data in a database.

### **Create (Insert Data):**
```php
$sql = "INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com')";
$conn->query($sql);
```

### **Read (Fetch Data):**
```php
$sql = "SELECT * FROM users";
$result = $conn->query($sql);
while($row = $result->fetch_assoc()) {
    echo $row['name']." - ".$row['email'];
}
```

### **Update Data:**
```php
$sql = "UPDATE users SET email='newemail@example.com' WHERE name='John Doe'";
$conn->query($sql);
```

### **Delete Data:**
```php
$sql = "DELETE FROM users WHERE name='John Doe'";
$conn->query($sql);
```

---
## 8. **Setting Query Parameters & Executing Queries in MySQL**
### **Definition:**
Query parameters allow dynamic execution of SQL statements, preventing SQL injection and improving security.

### **Using Prepared Statements:**
```php
$stmt = $conn->prepare("INSERT INTO users (name, email) VALUES (?, ?)");
$stmt->bind_param("ss", $name, $email);
$name = "Jane Doe";
$email = "jane@example.com";
$stmt->execute();
```

---
## 9. **PHP Joins Operations**
### **Definition:**
Joins allow retrieving related data from multiple tables by linking them using a common key.

### **Inner Join:**
Returns records that have matching values in both tables.
```php
$sql = "SELECT users.name, orders.order_id FROM users INNER JOIN orders ON users.id = orders.user_id";
$result = $conn->query($sql);
```

### **Left Join:**
Returns all records from the left table and matched records from the right table.
```php
$sql = "SELECT users.name, orders.order_id FROM users LEFT JOIN orders ON users.id = orders.user_id";
```

### **Right Join:**
Returns all records from the right table and matched records from the left table.
```php
$sql = "SELECT users.name, orders.order_id FROM users RIGHT JOIN orders ON users.id = orders.user_id";
```

### **Full Join (Not supported in MySQL, simulated with UNION):**
Returns all records when there is a match in either left or right table.
```php
$sql = "SELECT users.name, orders.order_id FROM users LEFT JOIN orders ON users.id = orders.user_id
        UNION
        SELECT users.name, orders.order_id FROM users RIGHT JOIN orders ON users.id = orders.user_id";
```

### **Self Join:**
Joins a table with itself using aliasing.
```php
$sql = "SELECT a.name AS Employee, b.name AS Manager FROM employees a INNER JOIN employees b ON a.manager_id = b.id";
```

### **Cross Join:**
Returns the Cartesian product of both tables (combines all rows).
```php
$sql = "SELECT users.name, orders.order_id FROM users CROSS JOIN orders";
```

---
## **Conclusion:**
- **Sessions** store temporary user data across pages on the server.
- **Cookies** store persistent data on the client side for tracking and personalization.
- **MySQL operations** enable efficient database management and integration with PHP.
- **Joins** help in retrieving relational data from multiple tables efficiently.

**AJAX in PHP**

## 1. **Introduction to AJAX**
### **Definition:**
AJAX (Asynchronous JavaScript and XML) is a technique used to update parts of a web page without reloading the entire page. It allows smooth and dynamic interactions between the user and the server, improving the user experience.

### **Key Features of AJAX:**
- Asynchronous request handling
- Reduces server load and bandwidth usage
- Enhances user experience with faster updates
- Supports various data formats (JSON, XML, HTML, Text)

---
## 2. **AJAX Model**
### **Working of AJAX:**
1. The user interacts with a webpage element (e.g., clicks a button).
2. JavaScript creates an `XMLHttpRequest` object.
3. The request is sent to the server asynchronously.
4. The server processes the request and sends back a response.
5. JavaScript receives the response and updates the webpage dynamically without reloading.

### **AJAX Workflow Diagram:**
```
User Action → JavaScript (XMLHttpRequest) → Server Process → Response → JavaScript Updates Page
```

---
## 3. **Implementation of AJAX in PHP**
### **Example: Fetching Data from MySQL using AJAX**

#### **Step 1: Create the Server-Side PHP Script (`fetch_data.php`)**
```php
<?php
header("Content-Type: application/json");
$conn = new mysqli("localhost", "root", "", "my_database");
$result = $conn->query("SELECT * FROM users");
$data = $result->fetch_all(MYSQLI_ASSOC);
echo json_encode($data);
?>
```

#### **Step 2: Create the JavaScript AJAX Request**
```javascript
fetch("fetch_data.php")
    .then(response => response.json())
    .then(data => console.log(data));
```

### **Example: Sending Data to Server with AJAX**

#### **Step 1: Create the HTML Form**
```html
<form id="userForm">
    <input type="text" id="name" name="name" placeholder="Enter Name">
    <input type="email" id="email" name="email" placeholder="Enter Email">
    <button type="submit">Submit</button>
</form>
```

#### **Step 2: JavaScript to Send Data to Server**
```javascript
document.getElementById("userForm").addEventListener("submit", function(event) {
    event.preventDefault();
    let formData = new FormData(this);
    fetch("save_data.php", {
        method: "POST",
        body: formData
    })
    .then(response => response.text())
    .then(data => console.log(data));
});
```

#### **Step 3: Server-Side Script (`save_data.php`)**
```php
<?php
$conn = new mysqli("localhost", "root", "", "my_database");
$name = $_POST['name'];
$email = $_POST['email'];
$conn->query("INSERT INTO users (name, email) VALUES ('$name', '$email')");
echo "Data saved successfully!";
?>
```

---
## **Conclusion**
- AJAX enables real-time communication between client and server.
- It improves performance and user experience by avoiding full page reloads.
- It is widely used in modern web applications for dynamic content updates.

