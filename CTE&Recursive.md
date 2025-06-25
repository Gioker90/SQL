# CTE&Recursive Queries
### Task: performing advanced calculation on previously created db [Company DB](https://github.com/Gioker90/SQL/blob/328f6cae24be7877e64e282a93f8b024b47ad4a2/DB%20%26%20tables%20Creation_Sales.md)

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
