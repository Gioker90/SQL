# CTE&Recursive Queries
### Task: performing advanced calculation on previously created db [Company DB](https://github.com/Gioker90/SQL/blob/328f6cae24be7877e64e282a93f8b024b47ad4a2/DB%20%26%20tables%20Creation_Sales.md)

Assuming that there is no duplicates value in our tables, I perform some CTEs on the data contained in the three tables

1. Using CTE to calculate the average of a sum. In this case I use the inner query to calculate the revenues of every store, and the outer query to know the average revenues across all the stores

```sql
WITH temp as (
  SELECT
    store_id,
    SUM(totalamount) as revenue
  FROM Sales
  GROUP by store_id
)
SELECT
  AVG(revenue) as avg
FROM temp
```
Result

![Screenshot 2025-06-25 165911](https://github.com/user-attachments/assets/b9408747-a883-4d12-b819-91d5d346fc88)

2. In the previous query I used one CTE- I can use mulitple CTEs to select different groups of items. in this case, I use 2 CTEs to select stores that perfrom well, meaning with >30000 uniqe sale and with more than 4 sales done, and an outer query with `UNION` to see all the stores with these criteria in the same Column

```sql
WITH temp as (
  SELECT
    sa.storeid,
	  s.location
  FROM Sales as sa
	  JOIN stores as s ON s.StoreID=Sa.StoreID
  WHERE totalamount>30000
),
   
temp1 (StoreID, Loc) as (
  SELECT
    sa.Storeid,
    s.location
  FROM Sales as sa
	  JOIN stores as s ON s.StoreID=Sa.StoreID
  GROUP BY sa.storeid
  HAVING count(sa.StoreID)>4
)
  
SELECT*
FROM temp  
UNION 
SELECT*
FROM temp1
```
Result

![Screenshot 2025-06-27 113257](https://github.com/user-attachments/assets/75ac1bbb-1e36-45dd-8f2e-fd5bebf2abeb)
