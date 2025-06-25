# Database and Table creation
#### Task: I want to create a databse containing the data of 52 employees of an hypothetical company; I want the data to have certain characteristics, so that I could perform some insightful analysis on them: every employee needs to have a uniqe ID, Name, work start date, if they lived the company, salary, birth date, gender, job role, deparment and termination date. The data with offices' information will be stored in another table, called "Office"

In order to do that I will create a db, using `CREATE DATABASE` anc calling it "HR"
```sql
CREATE DATABASE HR
```
Thereafter, I will use `CREATE TABLE` to define the type of data I want
````sql
CREATE TABLE HC (
ID int not null, 
	First_Name varchar(50), 
	Last_Name varchar(50), 
	Location varchar(50), 
	Start_date date,
	Attrition varchar(50), 
	Salary decimal (10, 2), 
	Birth_date date,
	Gender varchar(50), 
	Job_role varchar(50), 
	Department varchar(50),
	Termination_date date,
  	office_id int,
   	FOREIGN key (office_id) REFERENCES office(ID)
	Primary key (ID)
   )
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
SELECT *
FROM HC
````
Result

![Screenshot 2025-05-23 150613](https://github.com/user-attachments/assets/fec03796-c62c-49a8-a757-06679b9cc4f7)


#

Now I'll create a second table, called "Office", where the address and the location of the offices of the company will be stored
````sql
CREATE TABLE office(
   ID int not null,
   Office varchar(50),
   Address varhcar(100),
  PRIMARY key (ID)
  )
````
Populating the table leveraging AI, as previously done
````sql
INSERT INTO office (ID, Office, Address) VALUES
(1, 'Berlin', 'Friedrichstraße 43-45, 10117 Berlin, Germany'),
(2, 'Paris', '10 Rue de Rivoli, 75001 Paris, France'),
(3, 'Milan', 'Corso Buenos Aires 1, 20124 Milan, Italy'),
(4, 'Madrid', 'Calle de Alcalá 50, 28014 Madrid, Spain'),
(5, 'Lyon', 'Rue de la République 1, 69001 Lyon, France'),
--other 41 offices data
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

![Screenshot 2025-05-23 150747](https://github.com/user-attachments/assets/f69d8d9f-ab0a-400c-b982-fd5f22c8acbd)

