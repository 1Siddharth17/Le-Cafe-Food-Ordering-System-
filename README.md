# ☕ LE CAFÉ — Food Ordering System

A web-based **Food Ordering and Restaurant Management System** developed using **PHP, MySQL, HTML, CSS, and Bootstrap**. The system allows customers to browse food items, manage their shopping cart, and place orders, while managers can securely manage restaurant food items.

---

## 📌 Project Overview

**Le Café** is a database-driven web application designed to digitize the food ordering process for a restaurant.

The application provides two major user roles:

* 👤 **Customer** — Browse food items, add items to cart, manage quantities, and checkout.
* 👨‍💼 **Manager** — Log in to the management section and add new food items associated with their restaurant.

The project demonstrates the integration of **PHP server-side programming with MySQL database management**, along with session-based authentication and Bootstrap-based responsive UI.

---

## ✨ Features

### 👤 Customer Features

* Customer authentication and session management
* Browse available food items
* Add food items to shopping cart
* Manage cart items
* Remove individual items from cart
* Empty the entire cart
* Automatically calculate order total
* Checkout functionality
* Order confirmation with generated order number

### 👨‍💼 Manager Features

* Manager authentication
* Session-protected management pages
* Add new food items
* Specify:

  * Food name
  * Food price
  * Food description
  * Food image path
* Associate food items with the manager's restaurant

### 🗄️ Database Features

* MySQL database integration
* Dynamic retrieval of restaurant and food information
* Insertion of new food records
* Relationship between managers, restaurants, and food items

### 🎨 UI Features

* Responsive interface using Bootstrap
* Navigation based on user login status
* Simple and user-friendly food ordering interface

---

## 🛠️ Technology Stack

| Technology       | Purpose                         |
| ---------------- | ------------------------------- |
| **PHP**          | Server-side application logic   |
| **MySQL**        | Database management             |
| **HTML5**        | Web page structure              |
| **CSS3**         | Styling                         |
| **Bootstrap**    | Responsive UI                   |
| **JavaScript**   | Client-side functionality       |
| **Apache/XAMPP** | Local web server                |
| **mysqli**       | PHP-MySQL database connectivity |

---

## 🏗️ System Architecture

The application follows a basic three-layer architecture:

```text
             ┌──────────────────────┐
             │      User / Client   │
             │  Browser Interface   │
             └──────────┬───────────┘
                        │
                        ▼
             ┌──────────────────────┐
             │      PHP Layer       │
             │ Application Logic    │
             │ Sessions / Cart      │
             └──────────┬───────────┘
                        │
                        ▼
             ┌──────────────────────┐
             │     MySQL Database   │
             │  Users / Restaurants │
             │       / FOOD         │
             └──────────────────────┘
```

---

## 🗃️ Database

The project uses a MySQL database named:

```text
foodorder
```

The database contains tables representing important entities such as:

```text
MANAGER
    │
    │
    ▼
RESTAURANTS
    │
    │
    ▼
FOOD
```

### Important Tables

#### MANAGER

Stores manager-related information and authentication details.

#### RESTAURANTS

Stores restaurant information and associates a restaurant with its manager.

#### FOOD

Stores food items available at the restaurant.

Typical food information includes:

```text
Food ID
Food Name
Price
Description
Restaurant ID
Image Path
```

---

## ⚙️ Installation & Setup

Follow these steps to run the project locally.

### 1. Install XAMPP

Install **XAMPP** or another PHP/MySQL development environment.

Start:

```text
Apache
MySQL
```

---

### 2. Clone or Copy the Project

Place the project inside the XAMPP `htdocs` directory.

Example:

```text
C:\xampp\htdocs\LE-CAFE\
```

---

### 3. Create the Database

Open:

```text
http://localhost/phpmyadmin
```

Create a database named:

```text
foodorder
```

Import the project's SQL database file if one is provided.

---

### 4. Configure Database Connection

Open:

```text
connection.php
```

The current project configuration uses:

```php
Host: localhost
Username: root
Password: root
Database: foodorder
Port: 3308
```

Example configuration:

```php
$servername = "localhost";
$username = "root";
$password = "root";
$dbname = "foodorder";
$port = 3308;
```

> **Note:** MySQL commonly runs on port `3306`. If your local MySQL installation uses `3306`, update the connection configuration accordingly.

---

### 5. Add Food Images

Food images should be placed in the project's image directory.

Example:

```text
images/
├── burger.jpg
├── pizza.jpg
├── coffee.jpg
└── sandwich.jpg
```

When adding a food item, the image path should follow the expected format:

```text
images/filename.extension
```

Example:

```text
images/pizza.jpg
```

---

### 6. Run the Application

Open the project through your browser:

```text
http://localhost/LE-CAFE/
```

Depending on the project's entry page, you may need to open the appropriate PHP file directly.

---

## 🔐 Authentication & Sessions

The system uses PHP sessions to maintain user authentication and application state.

### Manager Session

Manager authentication is handled using:

```text
session_m.php
```

The manager session uses:

```php
$_SESSION['login_user1']
```

Management pages verify that a manager is logged in before allowing access.

If the manager is not authenticated, the system redirects the user to:

```text
managerlogin.php
```

### Customer Session

Customer information is maintained using:

```php
$_SESSION['login_user2']
```

The customer must be authenticated to access the shopping cart and checkout functionality.

---

## 🛒 Shopping Cart Workflow

The shopping cart is maintained using a PHP session array:

```php
$_SESSION["cart"]
```

A cart item contains information such as:

```text
Food ID
Food Name
Food Price
Restaurant ID
Food Quantity
```

### Cart Operations

#### Add Item

```text
Food Item
    ↓
Add to Cart
    ↓
$_SESSION["cart"]
```

#### Delete Item

The system supports deleting an individual food item using:

```text
?action=delete&id=<food_id>
```

#### Empty Cart

The complete cart can be cleared using:

```text
?action=empty
```

---

## 💳 Checkout Workflow

The basic checkout process follows:

```text
Customer Login
      ↓
Browse Food
      ↓
Add Food to Cart
      ↓
View Cart
      ↓
Calculate Total
      ↓
Checkout
      ↓
Payment / COD
      ↓
Order Confirmation
```

After successful checkout, the customer's session cart is cleared.

The COD page displays:

```text
Order Placed Successfully
```

An order number is also generated for confirmation.

---

## 👨‍💼 Manager — Add Food Workflow

The manager can add food items through:

```text
add_food_items.php
```

The form accepts:

```text
Food Name
Food Price
Food Description
Food Image Path
```

The form submits the information to:

```text
add_food_items1.php
```

The processing flow is:

```text
Manager Login
      ↓
Add Food Form
      ↓
Validate Manager Session
      ↓
Retrieve Restaurant ID
      ↓
Insert Food Record
      ↓
FOOD Table
      ↓
Redirect to Add Food Page
```

The restaurant ID is retrieved using the logged-in manager's information before inserting the food record.

---

## 🔄 Database Operation Example

The application retrieves the restaurant associated with the manager using a query similar to:

```sql
SELECT RESTAURANTS.R_ID
FROM RESTAURANTS, MANAGER
WHERE RESTAURANTS.M_ID = '$user_check';
```

A new food item is then inserted into the `FOOD` table:

```sql
INSERT INTO FOOD
(name, price, description, R_ID, images_path)
VALUES
('Food Name', '100', 'Food Description', '1', 'images/food.jpg');
```

---

## 🔒 Security

The project includes basic security mechanisms such as:

* Session-based authentication
* Restricted manager pages
* Input sanitization using `real_escape_string()`
* Separation of manager and customer sessions

Example:

```php
$conn->real_escape_string($input);
```

### ⚠️ Security Improvement

For a production-level application, all SQL queries should use **prepared statements** rather than string concatenation.

For example:

```php
$stmt = $conn->prepare(
    "INSERT INTO FOOD
    (name, price, description, R_ID, images_path)
    VALUES (?, ?, ?, ?, ?)"
);
```

Prepared statements provide stronger protection against SQL injection.

---

## 📋 Functional Requirements

1. Manager Login and Authentication
2. Customer Login and Authentication
3. Add Food Item
4. View Food Items
5. Add Items to Cart
6. Remove Items from Cart
7. Empty Cart
8. Calculate Order Total
9. Checkout
10. Generate Order Confirmation

---

## 📋 Non-Functional Requirements

### Security

The system should protect authenticated management functionality and prevent unauthorized access.

### Usability

The interface should be simple, responsive, and easy to navigate.

### Reliability

PHP sessions are used to maintain login and cart information during a user's interaction with the application.

### Maintainability

The application separates important functionality into individual PHP files such as database connection, session management, cart management, and checkout.

---

## 🚀 Future Enhancements

The current system provides the basic functionality required for a food ordering application. It can be extended with the following features.

### 1. Complete Food CRUD

Implement:

```text
Create
Read
Update
Delete
```

Currently, the major implemented management operation is adding food items.

Future pages could include:

```text
edit_food_items.php
delete_food_items.php
```

---

### 2. Persistent Order Management

Currently, checkout clears the session cart.

A production-ready version should permanently store orders in the database.

A possible design:

```text
CUSTOMER
    │
    ▼
ORDERS
    │
    ▼
ORDER_ITEMS
    │
    ▼
FOOD
```

The order should store information such as:

```text
Order ID
Customer ID
Restaurant ID
Order Date
Total Amount
Order Status
Payment Method
```

---

### 3. Customer Account Management

Add functionality for customers to:

* View profile
* Edit profile
* Change password
* View previous orders
* Track current orders

---

### 4. Order Tracking

Introduce order statuses such as:

```text
Placed
    ↓
Confirmed
    ↓
Preparing
    ↓
Out for Delivery
    ↓
Delivered
```

---

### 5. Improved Security

Future versions should implement:

* Prepared SQL statements
* Password hashing
* CSRF protection
* Input validation
* Secure session configuration
* Role-based authorization

---

### 6. Restaurant Management

Complete the restaurant management functionality so managers can:

* Add restaurant information
* Edit restaurant information
* View restaurant details
* Manage restaurant menu

---

## 📸 Screenshots

Add screenshots of the application here after running the project.

Example:

```text
screenshots/
├── home.png
├── login.png
├── food-menu.png
├── cart.png
├── checkout.png
└── manager-panel.png
---
## 📊 Project Highlights

* **Backend:** PHP
* **Database:** MySQL
* **Frontend:** HTML, CSS & Bootstrap
* **Authentication:** PHP Sessions
* **Cart:** PHP Session Array
* **Database Connectivity:** mysqli
* **Application Type:** Web-based Food Ordering System
* **Primary Database:** `foodorder`

---

## 🎯 Learning Outcomes

Through this project,I gained practical understanding of:

* PHP web application development
* MySQL database connectivity
* SQL queries and database operations
* Session management
* Authentication and authorization
* CRUD concepts
* Shopping cart implementation
* Database-driven dynamic content
* Bootstrap responsive design
* Basic web application security


# ☕ LE CAFÉ

### *A simple digital solution for restaurant food ordering and management.*

