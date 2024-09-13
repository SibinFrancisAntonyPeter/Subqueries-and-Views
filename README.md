# Subqueries-and-Views
# USING COUNTRY TABLE AND PERSON TABLE

SELECT * FROM Country;
SELECT * FROM Persons;

# 1. Find the number of persons in each country.

SELECT Country_name, COUNT(*) AS NumberofPersons FROM Persons
GROUP BY Country_name;

# 2. Find the number of persons in each country sorted from high to low. 

SELECT Country_name, COUNT(*) AS NumberofPersons FROM Persons
GROUP BY Country_name 
ORDER BY NumberOfPersons DESC;

# 3. Find out an average rating for Persons in respective countries if the average is greater than 3.0 

SELECT Country_name, AVG(Rating) AS AverageRating FROM Persons
GROUP BY Country_name
HAVING AverageRating > 3.0 ;

# 4. Find the countries with the same rating as the USA. (Use Subqueries)

SELECT Country_name
FROM Persons
WHERE Rating = (SELECT Rating FROM Persons WHERE Country_name = 'USA');

# 5. Select all countries whose population is greater than the average population of all nations. 

SELECT Country_name
FROM Country
WHERE Population > (SELECT AVG(Population)FROM Country);

# VIEWS 

CREATE DATABASE Product ;
USE Product ;

CREATE TABLE Customer(
 Customer_Id INT PRIMARY KEY,
 First_name VARCHAR(25),
 Last_name VARCHAR(25),
 Email VARCHAR(100),
 Phone_no VARCHAR (15),
 Address VARCHAR (100),
 City VARCHAR (50),
 State VARCHAR (50),
 Zip_code VARCHAR(10),
 Country VARCHAR (50)
 );
 
INSERT INTO Customer (Customer_Id, First_name, Last_name, Email, Phone_no, Address, City, State, Zip_code, Country)
VALUES 
(1, 'John', 'Doe', 'john.doe@example.com', '+1-2025550908', '123 Elm St', 'Los Angeles', 'California', '90001', 'USA'),
(2, 'Jane', 'Smith', 'jane.smith@example.com', '+1-2026650188', '456 Maple Ave', 'New York', 'New York', '10001', 'USA'),
(3, 'Michael', 'Johnson', 'm.johnson@example.com', '+1-2025550188', '789 Oak Blvd', 'Chicago', 'Illinois', '60601', 'USA'),
(4, 'Aisha', 'Patel', 'aisha.patel@example.com', '+61-412345678', '321 George Street', 'Sydney', 'New South Wales', '2000', 'Australia'),
(5, 'Vikram', 'Singh', 'vikram.singh@example.com', '+49-15209876543', '654 Hauptstrasse', 'Berlin', 'Berlin', '10115', 'Germany'),
(6, 'Sanya', 'Reddy', 'sanya.reddy@example.com', '+33-612345678', '987 Rue de Rivoli', 'Paris', 'Île-de-France', '75001', 'France'),
(7, 'Rohit', 'Bose', 'rohit.bose@example.com', '+81-9098765432', '123 Shibuya Crossing', 'Tokyo', 'Tokyo', '150-0001', 'Japan'),
(8, 'Sneha', 'Gupta', 'sneha.gupta@example.com', '+27-723456789', '456 Nelson Mandela Blvd', 'Cape Town', 'Western Cape', '8001', 'South Africa'),
(9, 'Manish', 'Verma', 'manish.verma@example.com', '+55-11987654321', '789 Avenida Paulista', 'São Paulo', 'São Paulo', '01310-100', 'Brazil'),
(10, 'Anjali', 'Desai', 'anjali.desai@example.com', '+91-9988776655', '321 Banjara Hills', 'Hyderabad', 'Telangana', '500034', 'India');

SELECT * FROM Customer;
 
 # 1. Create a view named customer_info for the Customer table that displays Customer’s Full name and email address. 
 # Then perform the SELECT operation for the customer_info view. 
 
CREATE VIEW customer_info AS 
SELECT CONCAT(First_name, ' ', Last_name) AS Full_name, Email
FROM Customer;

SELECT * FROM customer_info;

# 2. Create a view named US_Customers that displays customers located in the US.

CREATE VIEW US_Customers AS 
SELECT * FROM Customer
WHERE Country = 'USA';

SELECT * FROM US_Customers;

# 3. Create another view named Customer_details with columns full name(Combine first_name and last_name), email, phone_no, and state. 

CREATE VIEW Customer_details AS 
SELECT CONCAT(First_name, ' ', Last_name) AS Full_name, Email, Phone_no, State
FROM Customer;

SELECT * FROM Customer_details;

# 4. Update phone numbers of customers who live in California for Customer_details view. 

SET SQL_SAFE_UPDATES = 0;
UPDATE Customer
SET Phone_no = '+1-2029999999'
WHERE State = 'California';

# 5. Count the number of customers in each state and show only states with more than 5 customers.

SELECT State, COUNT(*) AS Customercount FROM Customer
GROUP BY State
HAVING Customercount > 5 ;

# 6. Write a query that will return the number of customers in each state, based on the "state" column in the "customer_details" view. 

SELECT State, COUNT(*) AS Customercount 
FROM Customer_details
GROUP BY State;

#  7. Write a query that returns all the columns from the "customer_details" view, sorted by the "state" column in ascending order.

SELECT * FROM Customer_details
ORDER BY State ASC;










