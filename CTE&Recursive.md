# Data Exploration
### Task: performing advanced calculation on previously created db [Company DB](https://github.com/Gioker90/SQL/blob/328f6cae24be7877e64e282a93f8b024b47ad4a2/DB%20%26%20tables%20Creation_Sales.md) and performing some analysis on it

Assuming that there is no duplicates value in our tables, I perform some CTEs on the data contained in the three tables

1. Using CTE to calculate the average os a sum. In this case I use the inner query to calculate the revenues of every store, and the outer query to know the average revenues across all the stores

```sql
with temp as (
  SELECT
store_id,
sum(totalamount) as revenue
from Sales
GROUP by store_id
  )
  SELECT
  avg(revenue) as avg
  from temp
```
Result

![Screenshot 2025-06-25 165911](https://github.com/user-attachments/assets/b9408747-a883-4d12-b819-91d5d346fc88)


.Streo with >40000$ revenues and less than 5 employees
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

4.Using `CASE` to split the population by Seniority, calculated as the difference between today and the start date
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
