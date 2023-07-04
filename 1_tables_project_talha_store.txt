-- 1.	Project: Online Store Database
-- •	Description: Create a database to store information about products, customers, orders, 
--         and inventory for an online store.

-- STEP 1: Create a Database which shows the Name of the Online Store (store name = talha_online)

CREATE DATABASE talha_online

-- Create Tables:
--   Table 1: Products: Contains information about products such as product ID, name, price, description, category, etc.

CREATE TABLE PRODUCTS (product_ID int PRIMARY KEY, Product_Name VARCHAR (300) UNIQUE, QUantity int, Price Decimal (10, 2), Description VARCHAR(1000),
			 Category VARCHAR (500) , Availability BOOLEAN , Creation_Date time, Last_Updates Time) 
			
-- Table 2 :  Customers: Stores customer details like customer ID, name, email, and address.

CREATE TABLE Customers (customer_id INT , First_Name VARCHAR (300), Last_Name VARCHAR (300), product_id int REFERENCES products (product_id), Email VARCHAR (300), Phone VARCHAR(20), Address VARCHAR (500),
						City VARCHAR (50), Province_or_State VARCHAR (50), Country VARCHAR (50), Post_Code VARCHAR (12), Joining_Date DATE
					   )
					   
-- Table 3:	Orders: Tracks orders placed by customers with information like order ID, customer ID, product ID, quantity, and order date.	

CREATE TABLE ORDERS (Order_ID INT PRIMARY KEY, customer_id INT , product_id INT REFERENCES products(product_id),
					 Quantity INT, order_date timestamp, total_price DECIMAL (10, 2))
					 
-- Table 4: Inventory: Manages the stock levels of products with details like product ID, quantity in stock, and last update date.

CREATE TABLE Inventory (Product_id INT REFERENCES products (product_id), stock_quantity INT PRIMARY KEY, Vendor_name VARCHAR(300), last_update_date DATE
							)
							
-- All four Tables are created But The Table:2(customers) is not relational table . To do so we need to ALTER the table

--In the first Step we will make the cloumn= customer_id as a primary key

--In the Second Step we will add another column in the table=customer i.e product_id make it relational by refrenceing it with the table=products and the cloumn=product_id relational

--First Step
ALTER TABLE customers ADD PRIMARY KEY (customer_id) ;

--Second Step
ALTER TABLE customers ADD COLUMN product_id INT REFERENCES products (product_id) ;



-- Now lets do some other operations on Database and Tables


--  1: To DELETE a DATABASE

DROP DATABASE talha_online

-- DROP DATABASE clause is used to DELETE the database. In the above example the DATABASE name is " talha_store"


-- 2: To DELETE a Table

DROP TABLE products

-- DROP Table clause is used to DELETE the Table. In the above example the DATABASE name is " product". But we cannot DELETE this table
-- because the column "product_id" is used in the RDBMS as a REFRENCES point in other TABLE.

DROP TABLE inventory

-- The "Inventory" Table is easy to delete because it does not have any REFRENCES directly involved

-- 3:Copy a table Duplicate
CREATE TABLE duplicate_products AS (SELECT * 
							   FROM products) 
							   
-- This query create a same table in seconds " CREATE TABLE" is the clause we use in the start of the query, 
-- later we give the name of the new tabe here the new name is "duplicate_products".
-- Thirds we use "AS" clause
-- Fourth we use subquery witha simple code which identify the table we wanted to make duplicate of .
-- Here we trying to make a duplicate of "product" table so the query will be (SELECT * FROM PRODUCTS)

-- 4: Change the name of the TABLE

ALTER TABLE duplicate_products RENAME TO products_two

--  Firstly, "ALTER TABLE" clause is used
--  Secondly The name of the table is mentioned which we want to rename. In this case table name is "duplicate_products"
--  Thirdly, use the clasue "Rename To"
--  Fourth, The name of the table which you want the output result . We choose therename name as "product_two" 

-- 5 : Add a new column in the existing Table

ALTER TABLE products_two ADD COLUMN new_inventory int

-- First We use the "ALTER TABLE" caluse
-- Secondly, we mention the name of the table we wanted to add the column . Here the name of the table is "products_two"
-- Third, we use the clause 'ADD COLUMN'
-- Fourth, we use the name of the new column we wanted to add including the type of the column "new_inventory int"

-- 6: Delete a column from a table

ALTER TABLE products_two DROP COLUMN new_inventory

-- First We use the "ALTER TABLE" caluse
-- Secondly, we mention the name of the table we wanted to delete the column from . Here the name of the table is "products_two"
-- Third, we use the clause 'DROP COLUMN'
-- Fourth, we use the name of the  column we wanted to delete including the type of the column "new_inventory int"

-- 7: Rename a column name
ALTER TABLE products_two RENAME COLUMN price to total_prices

-- First We use the "ALTER TABLE" caluse
-- Secondly, we mention the name of the table we wanted to use to change the name of the column from . Here the name of the table is "products_two"
-- Third, we use the clause 'Rename COLUMN'
-- Fourth,we mention the name of the current column name "price"
-- Fifth we used the clause "to"
-- Sixth, we mentioned the new name "total_prices"

-- 8: Change the data type of the column

ALTER TABLE products_two ALTER COLUMN total_prices TYPE int,
						 ALTER COLUMN quantity TYPE numeric(10, 2)	
						 
-- First We use the "ALTER TABLE" caluse
-- Secondly, we mention the name of the table we wanted to use to change the name of the column from . Here the name of the table is "products_two"
-- Third, we use the clause 'ALTER COLUMN'
-- Fourth,we mention the name of the  column "total_price"
-- Fifth we used the clause "TYPE" which leads us to the whcih data type we want to diplay 
-- Sixth, we mentioned the new data type desired "int"	
-- Seventh, We can do changes in two column in one command as well.

-- 9: Add 'Not NULL' constraints in a column
AlTER TABLE products_two ALTER COLUMN product_id SET NOT NULL

-- First We use the "ALTER TABLE" caluse
-- Secondly, we mention the name of the table we wanted to use to apply the "NOT NULL" constraint the name of the column from . Here the name of the table is "products_two"
-- Third, we use the clause 'ALTER COLUMN'
-- Fourth,we mention the name of the  column "product_id"
-- Fifth we used the clause "SET" 
-- Sixth, we mentioned "NOT NULL"

-- 10: Remove 'Not NULL' constraints in a column
ALTER TABLE products_two ALTER COLUMN product_id DROP NOT NULL

-- First We use the "ALTER TABLE" caluse
-- Secondly, we mention the name of the table we wanted to use to apply the "NOT NULL" constraint the name of the column from . Here the name of the table is "products_two"
-- Third, we use the clause 'ALTER COLUMN'
-- Fourth,we mention the name of the  column "product_id"
-- Fifth we used the clause "DROP" 
-- Sixth, we mentioned "NOT NULL"

-- 11: Change the Primary Key column
ALTER TABLE  products_two ADD PRIMARY KEY (quantity);  

-- First We use the "ALTER TABLE" caluse
-- Secondly, we mention the name of the table we using "products_two"
-- Third, we use the clause 'ADD PRIMARY KEY'
-- Fourth,we mention the name of the  column "quantity" . Do not forget to use prenthesis ().
-- Note: There can be only one Primary KEY (PK) in a table
-- Here in this table we changed the primary key from column "product_id" to "quantity"
