# Database and Table creation
#### Task: I want to create a databse containing the data of 52 employees of an hypothetical company; I want the data to have certain characteristics, so that I could perform some data analysis on them: every employee needs to have a uniqe ID, Name, work start date, if they lived the company, salary, birth date, gender, job role, deparment and termination date

In order to do that I will create a db, using `create db` anc calling it "HR"
```sql
create db HR
```
therefore I will use `create table` to define the type of data I want
````sql
create TABLE HC (
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
	Primary key (ID)
   )
````
Now I need to fill the table with data. To do that, I'll leverage AI to give me realistic data, specifing I want the termination dates only filled in the 7% of the employees (meaning the rest it's still in the company) - I then paste them with `insert into` as follows
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
