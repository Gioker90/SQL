# SQL
## Creation DB and Table
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
         start_date date, 
		attrition varchar(50), 
         Salary decimal (10, 2), 
         birth_date date,
         gender varchar(50), 
         job_role varchar(50), 
         department varchar(50),
termination_date date,
primary key (ID)
   )
````
Now I need to fill the data
