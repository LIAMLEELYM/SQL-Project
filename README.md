# Project of SQL Database Design - online rental company
After onesemester's study of the course "Database Management System",the database software introduced in this course is SQLserver and mysql, this paper will start with requirement analysis step bystep and design a simulation for a online rental company. This is the project that done with my groupmate during my postgraduate study.
## 1.Company Background
Friday Company is a recently established online rental company specializing in short-term leasing electronics, outdoor equipment, and luxury goods. The company offers a wide range of products in the electronics category, including the latest smartphones, tablets, photography equipment, headphones, speakers, televisions, and home appliances. Their outdoor equipment selection includes camping gear, hiking equipment, and more. The company offers high-end brand-name handbags, watches, and more in the luxury goods category.
The rental products on Friday Company's platform are sourced from their own inventory and third-party merchants. The company conducts quality inspections on the rental items provided by third-party merchants to ensure customer satisfaction. Their rental process is simple and convenient. Customers can browse their extensive product catalog on their website, select the items they are interested in, and determine the rental duration. The company takes care of the delivery and return process, with their inventory being shipped from their warehouse and third-party merchant items being shipped and returned by the merchants. This ensures a hassle-free rental experience for their customers.
At Friday Company, they are committed to providing high-quality products and prioritizing customer satisfaction and convenience. They offer 24-hour customer service support throughout the entire rental process to address any inquiries or concerns customers may have before and after their rental period. Whether you are an individual user or a corporate customer, Friday Company offers comprehensive rental solutions to meet your personalized needs.
## 2.Company problem
The goal at Friday Company is to establish a robust database that enables the seamless operation of their online rental system. This includes supporting customers in online product selection, providing round-the-clock customer service support, as well as tracking logistics information for both their warehouses and third-party storage facilities.
## 3.Conceptual DB Design
### 3.1 Entities, Attributes, and Relationships
Customer:
cu_id	Customer id
cu_name	Customer name
cu_pw	Customer password
cu_mail	Customer email
cu_pay	Customer payment
cu_level	Customer level
cu_po	Customer points
cu_quiz	Customer quiz to reset the password
cu_answer	Customer answer to reset the password
cu_type	Customer type
cu_address1	Customer address1
cu_address2	Customer address2
cu_address3	Customer address3

Subtype: Individual
in_realname	Individual realname
in_realid	Individual realid
in_birth	Individual birthday
in_gender	Individual gender

Subtype: Enterprise:
enter_taxID	Enterprise tax id
enter_name	Enterprise name

Customer Service:
help_id	Customer Service id
help_pw	Customer Service password
help_name	Customer Service name
help_gender	Customer Service gender
help_score	Customer Service score
help_contact	Customer service contact information
help_class	Customer Service class

Supplier:
shop_id	Supplier id
shop_name	Supplier name
shop_add	Supplier address
shop_license	Supplier license
shop_contact	Supplier contact information
shop_type	Supplier type (’Y’ means platform self-supplier, ’N’ means other supplier)

Subtype: Self Suppliers：
tank_id	Warehouse id


Subtype: Other Supplier:
entry_fee	Platform entry fee


Logistics Information:
exp_id	Logistics id
or_id	Order id
exp_now	Logistics status
exp_type	Logistics type
tank_id	Warehouse id

Commodity:
good_id	Good id
good_name	Good name
good_describe	Good description
good_price	Good price
class_id	Good class ID
class_name	Good class
brand_id	Good brand ID
brand_name	Good brand
good_left_Status(图片要改)	‘Y’ stand for available ,’N’ stand for unavailable


Warehouse:
tank_id	Warehouse id
tank_name	Warehouse name
tank_add	Warehouse address

After-sales Service Order:
job_id	After-sales Service id
order_id	Order id
job_content	After-sales Service content
job_now	After-sales Service status

Order:
or_id	Order id
or_now	Order status
cu_id	Customer id
or_add	Order address
or_price	Order price

Associate Entity:
Service Order:
help_id	Customer Service id
job_id	After-sales Service id
service date	Service date

Service Detail:
help_id	Customer Service id
cu_id	Customer id
service date	Service date

Order Detail:
or_id	Order id
or date	Order date
good_id	Good id

Supply Information:
good_id	Good id
shop_id	Supplier id
supply date	Supply date

Relationships:

Customer and Customer Service: many to many
Customer Service and After-sales Service Order: many to many
Order and After-sales Service Order: one to many
Customer and Order: one to many
Order and Commodity: many to many
Commodity and Supplier: many to many
Other Supplier and Logistics information: one to many
Self Supplier and Warehouse: one to many
Self Supplier and Logistics information: one to many
Order and Logistics information: one to many
### 3.2 ER Diagram
![image](https://github.com/LIAMLEELYM/SQL-Project/assets/166018789/14835ce0-2733-4bc6-a1e6-a83f91fb09fa)
## 4.Logical DB Design
### 4.1Relation vender
![image](https://github.com/LIAMLEELYM/SQL-Project/assets/166018789/2ab96871-49f1-4522-a3e4-c51fc5c66f08)
## 5. Physical Database Design
In the physical design, we chose SQLServer19 as the database management system. Based on the relationship model in logical design, we created the following tables:

Table Name:Class
Column Name Data Type Null is allowed or not?
class_id INT Not Allowed
class_name VARCHAR(255) Not Allowed
Table Name:Brand
Column Name Data Type Null is allowed or not?
brand_id INT Not Allowed
brand_name VARCHAR(255) Not Allowed
Table Name:Commodity
Column Name Data Type Null is allowed or not?
good_id INT Not Allowed
good_name VARCHAR(255) Not Allowed
shop_id INT Not Allowed
good_describe VARCHAR(255) Not Allowed
good_price DECIMAL(10, 2) Not Allowed
class_id INT Not Allowed
brand_id INT Not Allowed
good_status VARCHAR(1) Not Allowed
good_month INT Not Allowed
Table Name:Customer
Column Name Data Type Null is allowed or not?
cu_id INT Not Allowed
cu_name VARCHAR(255) Not Allowed
cu_telenum VARCHAR(255) Not Allowed
cu_pw VARCHAR(255) Not Allowed
cu_mail VARCHAR(255) Not Allowed
cu_level VARCHAR(255) Not Allowed
cu_po INT Not Allowed
cu_quiz VARCHAR(255) Not Allowed
cu_answer VARCHAR(255) Not Allowed
cu_type VARCHAR(255) Not Allowed
cu_address1 VARCHAR(255) Allowed
cu_address2 VARCHAR(255) Allowed
cu_address3 VARCHAR(255) Allowed
Table Name: Individual
Column Name Data Type Null is allowed or not?
cu_id INT Not Allowed
in_realname VARCHAR(255) Not Allowed
in_realid CHAR(18) Not Allowed
in_birth DATE Not Allowed
in_gender VARCHAR(255) Not Allowed
Table Name: Enterprise
Column Name Data Type Null is allowed or not?
cu_id INT Not Allowed
enter_taxID VARCHAR(255) Not Allowed
enter_name VARCHAR(255) Not Allowed
Table Name:CustomerService
Column Name Data Type Null is allowed or not?
help_id INT Not Allowed
help_pw VARCHAR(255) Not Allowed
help_name VARCHAR(255) Not Allowed
help_gender VARCHAR(255) Not Allowed
help_score DECIMAL(10, 2) Not Allowed
help_contact VARCHAR(255) Not Allowed
help_class VARCHAR(255) Not Allowed
Table Name:Supplier
Column Name Data Type Null is allowed or not?
shop_id INT Not Allowed
shop_add VARCHAR(255) Not Allowed
shop_add VARCHAR(255) Not Allowed
shop_contact VARCHAR(255) Not Allowed
shop_contact VARCHAR(255) Not Allowed
Table Name:SelfSuppliers
Column Name Data Type Null is allowed or not?
shop_id INT Not Allowed
tank_id INT Not Allowed
Table Name:OtherSupplier
Column Name Data Type Null is allowed or not?
shop_id INT Not Allowed
entry_fee DECIMAL(10, 2) Not Allowed
Table Name:Warehouse
Column Name Data Type Null is allowed or not?
tank_id INT Not Allowed
tank_name VARCHAR(255) Not Allowed
tank_add VARCHAR(255) Not Allowed
Table Name:Orders
Column Name Data Type Null is allowed or not?
or_id INT Not Allowed
or_now VARCHAR(255) Not Allowed
cu_id INT Not Allowed
or_add VARCHAR(255) Not Allowed
or_price DECIMAL(10, 2) Not Allowed
Table Name:AfterSalesServiceOrder
Column Name Data Type Null is allowed or not?
job_id INT Not Allowed
or_id INT Not Allowed
job_content VARCHAR(255) Not Allowed
job_now VARCHAR(255) Not Allowed
Table Name:ServiceOrder
Column Name Data Type Null is allowed or not?
job_id INT Not Allowed
help_id INT Not Allowed
service_date DATE Not Allowed
Table Name:ServiceDetail
Column Name Data Type Null is allowed or not?
cu_id INT Not Allowed
help_id INT Not Allowed
service_date DATE Not Allowed
Table Name:OrderDetail
Column Name Data Type Null is allowed or not?
or_id INT Not Allowed
good_id INT Not Allowed
or_date DATE Not Allowed
Table Name:SupplyInformation
Column Name Data Type Null is allowed or not?
shop_id INT Not Allowed
good_id INT Not Allowed
supply_date DATE Not Allowed
Table Name:Logistics_Information
Column Name Data Type Null is allowed or not?
exp_id INT Not Allowed
shop_id INT Not Allowed
tank_id INT Allowed
or_id INT Not Allowed
exp_now VARCHAR(255) Not Allowed
exp_type VARCHAR(255) Not Allowed

p_type VARCHAR(255) Not Allowed
## 6. Database Implementation
Based on previous design, we implemented database design with SQL scripting to create 
schemas and load data. We also analyzed the platform’s performance. The queries and results are as 
follows.
### 6.1 Create Table & Insert Value
#1. Class Table & Data
CREATE TABLE Class ( class_id INT PRIMARY KEY NOT NULL,
class_name VARCHAR(255) NOT NULL,);
INSERT INTO Class (class_id, class_name) VALUES
(1, 'Electronics'), (2, 'Luxury Bags'), (3, 'Sports Cars'),
(4, 'Smartphones'), (5, 'Watches'), (6, 'Laptops'),
(7, 'Cameras'), (8, 'Headphones'), (9, 'Gaming Consoles'),
(10, 'Drones');
#2. Brand Table & Data
CREATE TABLE Brand (
 brand_id INT PRIMARY KEY NOT NULL, brand_name VARCHAR(255) NOT NULL);
INSERT INTO Brand (brand_id, brand_name) VALUES
(1, 'Sony'),(2, 'Gucci'),(3, 'Ferrari'),(4, 'Apple'),
(5, 'Rolex'),(6, 'Nintendo'),(7, 'DJI');
#3. Commodity Table & Data
CREATE TABLE Commodity (
 good_id INT PRIMARY KEY NOT NULL, good_name VARCHAR(255) NOT NULL,
 shop_id INT NOT NULL, good_describe VARCHAR(255) NOT NULL,
 good_price DECIMAL(10, 2) NOT NULL, class_id INT NOT NULL,
 brand_id INT NOT NULL, good_status CHAR(1) NOT NULL,
 good_month INT NOT NULL,
 FOREIGN KEY (class_id) REFERENCES Class(class_id), 
 FOREIGN KEY (brand_id) REFERENCES Brand(brand_id) 
);
INSERT INTO Commodity (good_id, good_name, shop_id, good_describe, good_price, 
class_id, brand_id, good_status, good_month) VALUES
(1, '4K OLED TV', 1, '55-inch premium OLED TV', 29.9, 1, 1, 'Y', 6),
(2, 'Leather Handbag', 2, 'Genuine leather handbag', 39.9, 2, 2, 'Y', 8),
(3, 'Convertible Sports Car', 3, 'Two-seater with V8 engine', 49.9, 3, 3, 'Y', 10),
(4, 'iPhone 12 Pro', 4, 'Latest model with 5G', 99.9, 4, 4, 'N', 45),
(5, 'Luxury Watch', 5, 'Gold-plated, diamond-studded watch', 299, 5, 5, 'N', 36),
(6, 'Laptop', 3, 'High-performance with VR capability', 229.9, 6, 4, 'N', 48),
(7, 'DSLR Camera', 6, '24.2 MP with 4K video recording', 89.9, 7, 1, 'Y', 27),
(8, 'AirPods', 5, 'Wireless design', 34.9, 8,4 , 'N', 33),
(9, 'Switch Console', 6, 'Portable gaming console', 29.9, 9, 6, 'Y', 6),
(10, 'Quadcopter Drone', 5, 'With 4K camera and GPS', 79.9, 10, 7, 'Y', 6);
#4. Customer Table & Data
CREATE TABLE Customer (
 cu_id INT PRIMARY KEY NOT NULL, cu_name VARCHAR(255) NOT NULL,
 cu_telenum CHAR(11)NOT NULL, cu_pw VARCHAR(255) NOT NULL,
 cu_mail VARCHAR(255) NOT NULL, cu_pay VARCHAR(255) NOT NULL,
 cu_level VARCHAR(255) NOT NULL, cu_po INT NOT NULL,
 cu_quiz VARCHAR(255) NOT NULL, cu_answer VARCHAR(255) NOT NULL,
 cu_type VARCHAR(255) NOT NULL, cu_address1 VARCHAR(255) NOT NULL,
 cu_address2 VARCHAR(255) , cu_address3 VARCHAR(255));
INSERT INTO Customer (cu_id, cu_name, cu_telenum, cu_pw, cu_mail, cu_pay, cu_level, 
cu_po, cu_quiz, cu_answer, cu_type, cu_address1, cu_address2, cu_address3) VALUES
(11, 'Customer11', '13845678114', 'password0011', 'customer11@example.com', 'Credit Card', 
'Gold', 110, 'Favorite color?', 'Blue', 'Individual', '11 Main St', 'Apt 11', 'City11, Country11'),
(12, 'Customer12', '13645678122', 'password0012', 'customer12@example.com', 'Credit Card', 
'Silver', 120, 'Favorite color?', 'Red', 'Individual', '12 Main St', 'Apt 12', 'City12, Country12'),
(13, 'Customer13', '13545678137', 'password0013', 'customer13@example.com', 'Credit Card', 
'Gold', 130, 'Favorite color?', 'Blue', 'Individual', '13 Main St', 'Apt 13', 'City13, Country13'),
(14, 'Customer14', '13545678148', 'password0014', 'customer14@example.com', 'Credit Card', 
'Silver', 140, 'Favorite color?', 'Red', 'Individual', '14 Main St', 'Apt 14', 'City14, Country14'),
(15, 'Customer15', '13645678159', 'password0015', 'customer15@example.com', 'Credit Card', 
'Gold', 150, 'Favorite color?', 'Blue', 'Individual', '15 Main St', 'Apt 15', 'City15, Country15'),
(16, 'Customer16', '16667816553', 'password0016', 'customer16@example.com', 'Credit Card', 
'Silver', 160, 'Favorite color?', 'Red', 'Enterprise', '16 Main St', 'Apt 16', 'City16, Country16'),
(17, 'Customer17', '13245678179', 'password0017', 'customer17@example.com', 'Alipay', 
'Gold', 170, 'Favorite color?', 'Blue', 'Enterprise', '17 Main St', 'Apt 17', 'City17, Country17'),
(18, 'Customer18', '13045678186', 'password0018', 'customer18@example.com', 'Wechat Pay', 
'Silver', 180, 'Favorite color?', 'Red', 'Enterprise', '18 Main St', 'Apt 18', 'City18, Country18'),
(19, 'Customer19', '18667819357', 'password0019', 'customer19@example.com', 'Alipay', 
'Gold', 190, 'Favorite color?', 'Blue', 'Enterprise', '19 Main St', 'Apt 19', 'City19, Country19'),
(20, 'Customer20', '12345678201', 'password0020', 'customer20@example.com', 'Wechat Pay', 
'Silver', 200, 'Favorite color?', 'Red', 'Enterprise', '20 Main St', 'Apt 20', 'City20, Country20');
#5. Individual Table & Data
CREATE TABLE Individual (
 cu_id INT PRIMARY KEY, in_realname VARCHAR(255) NOT NULL,
 in_realid CHAR(18) NOT NULL, in_birth DATE NOT NULL,
 in_gender VARCHAR(255) NOT NULL,
 FOREIGN KEY (cu_id) REFERENCES Customer(cu_id));
INSERT INTO Individual (cu_id, in_realname, in_realid, in_birth, in_gender) VALUES
(11, 'John Doe11', 'ID000000000011', '1991-01-01', 'Male'),
(12, 'Jane Doe12', 'ID000000000012', '1992-01-01', 'Female'),
(13, 'John Doe13', 'ID000000000013', '1993-01-01', 'Male'),
(14, 'Jane Doe14', 'ID000000000014', '1994-01-01', 'Female'),
(15, 'John Doe15', 'ID000000000015', '1995-01-01', 'Male');
#6. Enterprise Table & Data
CREATE TABLE Enterprise( cu_id INT PRIMARY KEY, enter_taxID VARCHAR(20) 
NOT NULL, enter_name VARCHAR(255) NOT NULL, FOREIGN KEY (cu_id) 
REFERENCES Customer(cu_id));
INSERT INTO Enterprise (cu_id, enter_taxID, enter_name) VALUES
(16, 'TAX000000000016', 'Enterprise16'), (17, 'TAX000000000017', 'Enterprise17'),
(18, 'TAX000000000018', 'Enterprise18'), (19, 'TAX000000000019', 'Enterprise19'),
(20, 'TAX000000000020', 'Enterprise20');
#7. CustomerService Table & Data
CREATE TABLE CustomerService (
 help_id INT PRIMARY KEY NOT NULL, help_pw VARCHAR(255) NOT NULL,
 help_name VARCHAR(255) NOT NULL, help_gender VARCHAR(6) NOT NULL,
 help_score DECIMAL(10, 2) NOT NULL, help_contact VARCHAR(255) NOT NULL,
 help_class VARCHAR(255) NOT NULL);
INSERT INTO CustomerService (help_id, help_pw, help_name, help_gender, help_score, 
help_contact, help_class) VALUES
(1, 'service001', 'Service Agent 1', 'Female', 4.5, 'service1@example.com', 'Electronics'),
(2, 'service002', 'Service Agent 2', 'Male', 4.6, 'service2@example.com', 'Luxury Bags'),
(3, 'service003', 'Service Agent 3', 'Female', 4.7, 'service3@example.com', 'Sports Cars'),
(4, 'service004', 'Service Agent 4', 'Male', 4.8, 'service4@example.com', 'Smartphones'),
(5, 'service005', 'Service Agent 5', 'Female', 4.9, 'service5@example.com', 'Watches'),
(6, 'service006', 'Service Agent 6', 'Male', 3.4, 'service6@example.com', 'Laptops'),
(7, 'service007', 'Service Agent 7', 'Female', 4.3, 'service7@example.com', 'Cameras'),
(8, 'service008', 'Service Agent 8', 'Male', 4.2, 'service8@example.com', 'Headphones'),
(9, 'service009', 'Service Agent 9', 'Female', 3.8, 'service9@example.com', 'Gaming Consoles'),
(10, 'service010', 'Service Agent 10', 'Male', 4.0, 'service10@example.com', 'Drones');
#8. Supplier Table & Data
CREATE TABLE Supplier (
 shop_id INT PRIMARY KEY NOT NULL, shop_name VARCHAR(255) NOT NULL,
 shop_add VARCHAR(255) NOT NULL, shop_license VARCHAR(255) NOT NULL,
 shop_contact VARCHAR(255) NOT NULL, shop_type VARCHAR(255) NOT NULL);
INSERT INTO Supplier (shop_id, shop_name, shop_add, shop_license, shop_contact, 
shop_type) VALUES
(1, 'Supplier 1', '1 Supplier St', 'Lic001', 'contact1@example.com', 'Y'),
(2, 'Supplier 2', '2 Supplier St', 'Lic002', 'contact2@example.com', 'Y'),
(3, 'Supplier 3', '3 Supplier St', 'Lic003', 'contact3@example.com', 'Y'),
(4, 'Supplier 4', '4 Supplier St', 'Lic004', 'contact4@example.com', 'N'),
(5, 'Supplier 5', '5 Supplier St', 'Lic005', 'contact5@example.com', 'N'),
(6, 'Supplier 6', '6 Supplier St', 'Lic006', 'contact6@example.com', 'N');
#9. SelfSuppliers Table & Data
CREATE TABLE SelfSuppliers ( shop_id INT PRIMARY KEY NOT NULL, tank_id INT 
NOT NULL, FOREIGN KEY (shop_id) REFERENCES Supplier(shop_id));
INSERT INTO SelfSuppliers (shop_id, tank_id) VALUES (1, 1),(2, 2),(3, 3);
#10. OtherSupplier Table & Data
CREATE TABLE OtherSupplier (
 shop_id INT PRIMARY KEY NOT NULL, entry_fee DECIMAL(10, 2) NOT NULL,
 FOREIGN KEY (shop_id) REFERENCES Supplier(shop_id));
INSERT INTO OtherSupplier (shop_id, entry_fee) VALUES(4, 1000),(5, 2000),(6, 1500);
#11. Warehouse Table & Data
CREATE TABLE Warehouse ( tank_id INT PRIMARY KEY NOT NULL,
 tank_name VARCHAR(255) NOT NULL, tank_add VARCHAR(255) NOT NULL);
INSERT INTO Warehouse (tank_id, tank_name, tank_add) VALUES
(1, 'Warehouse 1', 'China,Gouangdong Province,Goungzhou'),
(2, 'Warehouse 2', 'China,Shanghai'), (3, 'Warehouse 3', 'China,Liaoning Province,Shenyang');
#12. Orders Table & Data
CREATE TABLE Orders (
 or_id INT PRIMARY KEY NOT NULL, or_now VARCHAR(255) NOT NULL,
 cu_id INT NOT NULL, or_add VARCHAR(255) NOT NULL,
 or_price DECIMAL(10, 2) NOT NULL,
 FOREIGN KEY (cu_id) REFERENCES Customer(cu_id));
INSERT INTO Orders (or_id, cu_id, or_add, or_now, or_price)
VALUES 
(21, 19, '431 Main St', 'in process',29.9), (22, 20, '432 Main St','finished', 39.9),
(23, 18, '433 Main St','in process', 49.9), (24, 17, '434 Main St', 'finished',99.9),
(25, 16, '435 Main St', 'in process',299), (26, 15, '436 Main St', 'finished', 229.9),
(27, 14, '437 Main St','in process', 89.9), (28, 13, '438 Main St', 'in process',34.9),
(29, 12, '439 Main St','in process', 29.9), (30, 20, '440 Main St','pending', 79.9);
#13. AfterSalesServiceOrder Table & Data
CREATE TABLE AfterSalesServiceOrder (
 job_id INT PRIMARY KEY NOT NULL, or_id INT NOT NULL,
 job_content VARCHAR(255) NOT NULL, job_now VARCHAR(255) NOT NULL,
 FOREIGN KEY (or_id) REFERENCES Orders(or_id));
INSERT INTO AfterSalesServiceOrder VALUES (22, 22, 'Description mismatch', 
'Completed');
INSERT INTO AfterSalesServiceOrder VALUES (23, 23, 'Refund', 'In Service');
INSERT INTO AfterSalesServiceOrder VALUES (25, 25, 'Repair', 'In Service');
INSERT INTO AfterSalesServiceOrder VALUES (26, 26, 'Refund', 'Completed');
INSERT INTO AfterSalesServiceOrder VALUES (27, 27, 'Repair', 'In Service');
INSERT INTO AfterSalesServiceOrder VALUES (28, 28, 'Repair', 'Completed');
INSERT INTO AfterSalesServiceOrder VALUES (29, 29, 'Repair', 'In Service');
#14. ServiceOrder Table & Data
CREATE TABLE ServiceOrder ( help_id INT NOT NULL,
 job_id INT NOT NULL, service_date DATE NOT NULL,
 FOREIGN KEY (help_id) REFERENCES CustomerService(help_id),
 FOREIGN KEY (job_id) REFERENCES AfterSalesServiceOrder(job_id));
INSERT INTO ServiceOrder VALUES (2, 22, '2024-03-29');
INSERT INTO ServiceOrder VALUES (3, 23, '2024-03-30');
INSERT INTO ServiceOrder VALUES (5, 25, '2024-04-01');
INSERT INTO ServiceOrder VALUES (6, 26, '2024-04-02');
INSERT INTO ServiceOrder VALUES (7, 27, '2024-04-03');
INSERT INTO ServiceOrder VALUES (8, 28, '2024-04-04');
INSERT INTO ServiceOrder VALUES (9, 29, '2024-04-05');
#15. ServiceDetail Table & Data
CREATE TABLE ServiceDetail ( help_id INT NOT NULL,
 cu_id INT NOT NULL, service_date DATE NOT NULL,
 FOREIGN KEY (help_id) REFERENCES CustomerService(help_id),
 FOREIGN KEY (cu_id) REFERENCES Customer(cu_id));
INSERT INTO ServiceDetail VALUES (2, 20, '2024-03-29');
INSERT INTO ServiceDetail VALUES (3, 18, '2024-03-30');
INSERT INTO ServiceDetail VALUES (4, 17, '2024-03-31');
INSERT INTO ServiceDetail VALUES (5, 16, '2024-04-01');
INSERT INTO ServiceDetail VALUES (6, 15, '2024-04-02');
INSERT INTO ServiceDetail VALUES (7, 14, '2024-04-03');
INSERT INTO ServiceDetail VALUES (8, 13, '2024-04-04');
INSERT INTO ServiceDetail VALUES (9, 12, '2024-04-05');
#16. OrderDetail Table & Data
CREATE TABLE OrderDetail (
 or_id INT NOT NULL, or_date DATE NOT NULL,
 good_id INT NOT NULL, FOREIGN KEY (or_id) REFERENCES Orders (or_id),
 FOREIGN KEY (good_id) REFERENCES Commodity(good_id));
INSERT INTO OrderDetail VALUES (21, '2024-03-27', 1);
INSERT INTO OrderDetail VALUES (22, '2024-03-27', 2);
INSERT INTO OrderDetail VALUES (23, '2024-03-27', 3);
INSERT INTO OrderDetail VALUES (24, '2024-03-27', 4);
INSERT INTO OrderDetail VALUES (25, '2024-03-27', 5);
INSERT INTO OrderDetail VALUES (26, '2024-03-27', 6);
INSERT INTO OrderDetail VALUES (27, '2024-03-27', 7);
INSERT INTO OrderDetail VALUES (28, '2024-03-27', 8);
INSERT INTO OrderDetail VALUES (29, '2024-03-27', 9);
INSERT INTO OrderDetail VALUES (30, '2024-03-27', 10);
#17. SupplyInformation Table & Data
CREATE TABLE SupplyInformation (
 good_id INT NOT NULL, shop_id INT NOT NULL,
 supply_date DATE NOT NULL, PRIMARY KEY (good_id, shop_id),
 FOREIGN KEY (good_id) REFERENCES Commodity(good_id),
 FOREIGN KEY (shop_id) REFERENCES Supplier(shop_id));
INSERT INTO SupplyInformation VALUES (1, 1, '2024-03-28');
INSERT INTO SupplyInformation VALUES (2, 2, '2024-03-29');
INSERT INTO SupplyInformation VALUES (4, 4, '2024-03-31');
INSERT INTO SupplyInformation VALUES (5, 5, '2024-03-29');
INSERT INTO SupplyInformation VALUES (7, 6, '2024-04-03');
INSERT INTO SupplyInformation VALUES (8, 5, '2024-04-04');
INSERT INTO SupplyInformation VALUES (10, 5, '2024-04-06');
#18. Logistics_Information Table & Data
CREATE TABLE Logistics_Information ( exp_id INT PRIMARY KEY NOT NULL,
 shop_id INT NOT NULL, tank_id INT, or_id INT NOT NULL,
exp_now VARCHAR(255) NOT NULL,
exp_type VARCHAR(255) NOT NULL,
 FOREIGN KEY (shop_id) REFERENCES Supplier(shop_id),
 FOREIGN KEY (tank_id) REFERENCES Warehouse(tank_id),
FOREIGN KEY (or_id) REFERENCES Orders(or_id));
INSERT INTO Logistics_Information (exp_id , shop_id , tank_id , or_id , exp_now, exp_type ) 
VALUES 
(01, 1,1, 21, 'Shipped','rent'), (02, 2,2, 22, 'Delivered','rent'), (04, 4,null, 24,'Shipped','rent'),
(05, 5,null, 25, 'Delivered','rent'), (07, 6,null, 27, 'Shipped','rent'),
(08, 5,null, 28, 'Delivered','rent'), (010,5,null, 22,'Shipped','rent'),
(12,2,1,26, 'Processing','return'), (15,5,null,25,'Processing','return');
