# Database and Table creation
#### Task: In order to perform some complex queries such CTEs and recursive queries, I will create a database with 3 differnt tables, called 'Employees', 'Sales', and 'Stores'

I'll firstly create a DB, using`CREATE DATABASE` and calling it "Company DB"
```sql
CREATE DATABASE Company DB
```
Thereafter, I will use `CREATE TABLE` to define the type of data I want in my tables
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
And then using `INSERT INTO` as follows, to populate thge table

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

Now I'll create a second table, called "Stores", where I'll store the information about sotres location and store's Manager
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

The 3rd table I'll create is called 'Employees' and it contatins employees information, included the ID of the direct supervior of every employee

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

Result

