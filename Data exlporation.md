# Data Exploration
### Task: exploring the data from a previously created db [HC](https://github.com/Gioker90/SQL/blob/09327297583407521845952ada44ebb3c18d44cc/DB%20%26%20table%20creation.md) and performing some analysis on it

- Looking for null or duplicate values

1.Using `COUNT` & `IS NULL` to look for null values in the ID column

```sql
SELECT
  COUNT(*) as 'Count of IDs'
FROM HC
WHERE id IS NULL
```
This will be the result: no null values

![Screenshot 2025-05-22 120240](https://github.com/user-attachments/assets/13bdbf62-f56f-419e-a889-77fb82cc88cb)

2.Using `COUNT` & `DISTINCT` to look for duplicate values in the ID column
```sql
SELECT
  COUNT(*)-COUNT(DISTINCT(id)) as' N° of Duplicate values'
FROM HC
```
This will be the result: no duplicates ID values

![Screenshot 2025-05-22 121207](https://github.com/user-attachments/assets/d1e58b5f-374d-4231-b732-e84cefd67e6a)
#

- Let's do some calculation

1.Using `AVG`, `ROUND` & `GROUP BY` to calculate average salary by Department
```sql
SELECT
department,
ROUND(AVG(salary),2) as 'Avg salary'
FROM HC
GROUP BY department
```
This will be the result

![Screenshot 2025-05-22 144543](https://github.com/user-attachments/assets/f30959a2-10db-4ac9-af9e-1908a114aabe)

2.Using `LIKE` to find employees whose last name start with "D" and that work in IT Department
```sql
SELECT
  first_name,
  last_name
FROM HC
WHERE last_name LIKE ('D%') AND department='IT'
```

This will be the result

![image](https://github.com/user-attachments/assets/fd71895a-a9c8-4f61-9d0a-11a468a71353)

3.Using `BETWEEN` to find the employees hired from 2016 to 2020 who didn't leave the company

```sql
SELECT
  first_name,
  last_name
FROM HC
WHERE (start_date BETWEEN '2016-01-01' AND '2020-31-12')
	AND
	attrition='No'
```
This will be the result

![Screenshot 2025-05-22 150353](https://github.com/user-attachments/assets/27c9bf42-5722-4f26-8f05-a47ba3f4f5d9)

4.Using `CASE` to split the population by Seniority, calculated like the difference between today and the start date
```sql
select
  CASE
    WHEN (CURRENT_DATE-start_date) <=3 THEN 'Junior'
    WHEN (CURRENT_DATE-start_date) <=5 THEN 'Intermediate'
    WHEN (CURRENT_DATE-start_date) <=8 THEN 'Senior'
    ELSE 'Expert'
  END AS Seniority,
COUNT(*) as HC
FROM HC
GROUP BY Seniority
```
This will be the result

![Screenshot 2025-05-22 143232](https://github.com/user-attachments/assets/34c2bc1a-3ea8-40be-98c2-5b56a86d5f47)

5.Using `COUNT`, `GROUP BY`, `UNION` & `ORDER BY` to see how many people left the company. I want to see the information grouped by city and in alphabetic order, and I also qant to see the total leavers
```sql
SELECT
  Location,
  COUNT(*) as Leavers
FROM HC
WHERE attrition='Yes'
GROUP BY department

UNION

SELECT
  'Total',
  COUNT(*)
FROM HC
WHERE attrition='Yes'
ORDER BY location ASC
```
This will be the result: 4 leavers in 4 different citites

![Screenshot 2025-05-22 122519](https://github.com/user-attachments/assets/2121df1c-8c16-4857-a19f-39dfcbd1b7c3)

6.I want to know who, in the IT department, is earning less then the average Salary in the same department. I'll use a subquery, to do that
```SQL
SELECT
  first_name,
  last_name,
  salary
FROM HC
WHERE salary < (SELECT avg(salary)
              FROM HC
              WHERE department='IT')
              AND department='IT'
ORDER by salary desc
```

This will be the result

![Screenshot 2025-05-22 152059](https://github.com/user-attachments/assets/3241a8a1-bcd1-480b-a018-b073a9e54520)





