# SQL Project – Clients and Products

This is my first SQL project using MySQL.  
I created a small database with clients and products to practice creating tables, adding data, and running queries.

---

## Step 1 – Create the Database

```sql
CREATE DATABASE Proyect_1;

Step 2 – Create the Tables

Clients table

sql
CREATE TABLE clients( 
    id_clients INT NOT NULL AUTO_INCREMENT, 
    name VARCHAR(50) NOT NULL, 
    surname VARCHAR(100), 
    email VARCHAR(100) NOT NULL, 
    quota ENUM("Premium", "Medium", "Low-Cheap"), 
    UNIQUE (id_clients), 
    PRIMARY KEY (id_clients)
);

Products table
sql
CREATE TABLE products (
    id_products INT NOT NULL,
    product VARCHAR(50),
    price DECIMAL(10,2),
    id_clients INT,
    PRIMARY KEY (id_products),
    UNIQUE (id_products),
    FOREIGN KEY (id_clients) REFERENCES clients(id_clients)
);

Step 3 – Add missing column
At first, I forgot to add the column age to the clients table, so I used this query:

sql
ALTER TABLE clients ADD COLUMN age INT;

Step 4 – Insert data
Example insert into the clients table:

sql
INSERT INTO clients (name, surname, age, email, quota)
VALUES ("Javier", "Gonzalez", 25, "Jgonzalez@gmail.com", "Premium");

When inserting into products, I got an error (1364) because I didn’t set the AUTO_INCREMENT.
I fixed it with this command:

sql
ALTER TABLE products MODIFY id_products INT NOT NULL AUTO_INCREMENT;
Then I added several products manually.

Step 5 – Products list

Headphones
Bagpack
Computer
Charger
Tablet
Car
Bike
TV
Music Speaker
TV Control

SQL Exercises

Exercise 1
Show the name, surname, and quota of all clients whose quota is not “Low-Cheap”, ordered alphabetically by surname.

sql
SELECT name, surname, quota
FROM clients
WHERE quota != "Low-Cheap"
ORDER BY surname ASC;

Exercise 2
Get the name and age of all clients who are between 25 and 35 years old.

sql
SELECT name, age
FROM clients
WHERE age BETWEEN 25 AND 35;

Exercise 3

Show all products together with the first name and last name of the client they belong to.
If a product doesn’t have a client, it should still appear in the results.

sql
SELECT name, surname, product
FROM products
LEFT JOIN clients
ON products.id_clients = clients.id_clients;

Exercise 4
Calculate how many products each client quota type has.

sql
SELECT quota,
COUNT(quota)
FROM clients
JOIN products
ON products.id_clients = clients.id_clients
GROUP BY quota;

Exercise 5
Calculate the average price of the products that belong to Premium clients.

sql
SELECT product,
AVG(price)
FROM clients
JOIN products
ON products.id_clients = clients.id_clients
WHERE quota = "Premium"
GROUP BY product;

Summary

Through this project I practiced:
Creating and modifying tables in MySQL
Using primary and foreign keys
Applying JOIN, GROUP BY, and aggregate functions

Fixing common SQL errors

Working with realistic data to simulate real-world cases
