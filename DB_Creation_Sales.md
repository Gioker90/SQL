# data

# Database and Table creation
#### Task: I want to create a databse containing the data of 52 employees of an hypothetical company; I want the data to have certain characteristics, so that I could perform some insightful analysis on them: every employee needs to have a uniqe ID, Name, work start date, if they lived the company, salary, birth date, gender, job role, deparment and termination date. The data with offices' information will be stored in another table, called "Office"

In order to do that I will create a db, using `CREATE DATABASE` anc calling it "Company_DB"
```sql
CREATE DATABASE Company_DB
```
Thereafter, I will use `CREATE TABLE` to define the type of data I want
````sql

CREATE TABLE Sales (
    SaleID INT PRIMARY KEY,
    SaleDate DATE,
    Description TEXT,
    Amount DECIMAL(10, 2),
    CustomerName VARCHAR(100),
    ProductID INT,
    Quantity INT,
    Discount DECIMAL(5, 2),
    TotalAmount DECIMAL(10, 2),
    StoreID INT,
    FOREIGN KEY (StoreID) REFERENCES Stores(StoreID)
);

````
Now I need to fill the table with data. To do that, I'll leverage AI to give me realistic data, specifing I want the termination dates only filled in the 7% of the employees (meaning the rest of the employees it's still in the company) - I then paste them with `INSERT INTO` as follows
````sql
INSERT INTO HC (ID, First_Name, Last_Name, Location, start_date, 
attrition, Salary, birth_date, gender, job_role, department, 
termination_date)
VALUES
(1, 'Hans', 'Schmidt', 'Berlin', '2018-06-15', 'Yes', 68000.00, 
'1985-03-12', 'Male', 'Senior Financial Analyst', 'Finance', '2023-07-28'),
(2, 'Sophie', 'Dubois', 'Paris', '2017-04-22', 'Yes', 72500.50, 
'1983-11-04', 'Female', 'Marketing Director', 'Marketing', '2023-02-15'),
(3, 'Marco', 'Rossi', 'Milan', '2019-01-10', 'Yes', 59000.75, 
'1990-08-23', 'Male', 'Software Developer', 'IT', '2022-11-30'),
(4, 'Elena', 'García', 'Madrid', '2016-09-05', 'Yes', 81200.25, 
'1979-03-17', 'Female', 'Human Resources Manager', 'HR', '2023-08-01')
--other 48 employees data
````
Now I'll use `SELECT` to explore the result
````sql
INSERT INTO Sales (ID, SaleDate, Description, Amount, CustomerName, ProductID, Quantity, Discount, TotalAmount, Store_ID) VALUES
(1, '2025-01-01', 'Product A', 100.00, 'Customer 1', 101, 2, 5.00, 190.00, 1),
(2, '2025-01-02', 'Product B', 150.00, 'Customer 2', 102, 1, 10.00, 140.00, 2),
(3, '2025-01-03', 'Product C', 200.00, 'Customer 3', 103, 3, 15.00, 585.00, 3),
(4, '2025-01-04', 'Product D', 250.00, 'Customer 4', 104, 4, 20.00, 980.00, 4),
(5, '2025-01-05', 'Product E', 300.00, 'Customer 5', 105, 5, 25.00, 1425.00, 5),
--other 39 Sales data

````
Result




#

Now I'll create a second table, called "Office", where the address and the location of the offices of the company will be stored
````sql
CREATE table Stores(
  StoreID int primary key,
  location text,
  Manager_First_Name varchar(100),  
  Manager_Last_Name varchar(100),
 Manager_ID INT,
  FOREIGN KEY (Manager_ID) REFERENCES Employees(supervisor_id)
);
````
Populating the table leveraging AI, as previously done
````sql
INSERT INTO Stores (StoreID, location, Manager_First_Name, Manager_Last_Name, Manager_ID) VALUES
(1, 'London, UK', 'John', 'Doe', 1),
(2, 'Paris, France', 'Jane', 'Smith', 2),
(3, 'Berlin, Germany', 'Michael', 'Johnson', 3),
(4, 'Madrid, Spain', 'Emily', 'Davis', 4),
(5, 'Rome, Italy', 'Chris', 'Brown', 5),
-- other 5 rows
````

Now I'll create a second table, called "Office", where the address and the location of the offices of the company will be stored
````sql
CREATE TABLE Employees (
    ID INT PRIMARY KEY,
    First Name VARCHAR(100),
    Last_Name VARCHAR(100),
    Supervisor_ID VARCHAR(100),
  FOREIGN key (Supervisor_ID) REFERENCES Stores(manager_id)
);
````
Populating the table leveraging AI, as previously done
````sql
INSERT INTO Employees (ID, First_Name, Last_Name, Supervisor_ID) VALUES
(1, 'John', 'Doe', 31),
(2, 'Jane', 'Smith', 31),
(3, 'Michael', 'Johnson', 31),
(4, 'Emily', 'Davis', 31),
(5, 'Chris', 'Brown', 31),
-- other 26 rows
````

ID is the primary key of the 'office' table. I need therfore to populate the column 'Office_id' in 'HC', and making it a foreign key. This will create a parent-child relationship that will ensure data integrity and consistency. I will use `UPDATE` `SET` for this scope
````sql
UPDATE HC
SET
office_id=(select id
	FROM office
	WHERE office.id=HC.office_id
)
````

Result

