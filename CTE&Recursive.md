# CTE&Recursive Queries
### Task: performing advanced calculation on previously created db [Company DB](https://github.com/Gioker90/SQL/blob/328f6cae24be7877e64e282a93f8b024b47ad4a2/DB%20%26%20tables%20Creation_Sales.md)

Assuming that there is no duplicates value in our tables, I perform some CTEs on the data contained in the three tables

1. Using CTE to calculate the average of a sum. In this case I'll use the inner query to calculate the revenues of every store, and the outer query to know the average revenues across all the stores

```sql
WITH temp as (
  SELECT
    store_id,
    SUM(totalamount) as revenue
  FROM Sales
  GROUP by store_id
)
SELECT
  AVG(revenue) as avg_revenues
FROM temp
```
Result

![Screenshot 2025-06-25 165911](https://github.com/user-attachments/assets/b9408747-a883-4d12-b819-91d5d346fc88)

2. In the previous query I used one CTE. I can use mulitple CTEs to select different groups of items. In this case, I use 2 CTEs to select stores that perform well, meaning that made a sale of >30000 with more than 4 sales done.
Then, I'll write the outer query with `UNION` clause to see all the stores with these criteria in the same Column

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

3. Now, to further analyze the best performing Stores, I want to select the ones that had bigger income than the average. In order to do that, I will use a nested CTE.
With the first inner query I select the total income for every Store, than, with the nested query, I calculate the average income across all the Stores.
Finally, with the outer query I'll select the stores that earn more than the average, including both the previous CTEs in the `FROM` clause

```sql

WITH temp as (
 SELECT
  S.StoreID,
  location,
  SUM(totalamount) as Store_Revenues
 FROM Sales as S
	JOIN Stores ON Stores.StoreID=S.StoreID
 GROUP BY S.StoreID
),

 temp1 as (
  SELECT
   AVG(Store_Revenues) as Overall_Avg
  FROM TEMP
)

SELECT
 location,
 Store_Revenues,
 Overall_avg
FROM temp, temp1
WHERE Store_Revenues > Overall_Avg
```
Result

![Screenshot 2025-06-27 151044](https://github.com/user-attachments/assets/dead8a53-58b4-4e41-a3ae-0744a25cc126)
