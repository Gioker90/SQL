# Data Exploration
### Task: exploring the data from a previously created db [HC](https://github.com/Gioker90/SQL/blob/09327297583407521845952ada44ebb3c18d44cc/DB%20%26%20table%20creation.md) and performing some analysis on it

- Looking for null or duplicate values

Using `COUNT` & `IS NULL` to look for null values in the ID column

```sql
SELECT
  COUNT(*) as 'Count of IDs'
FROM HC
WHERE id IS NULL
```
This will be the result: no null values

![Screenshot 2025-05-22 120240](https://github.com/user-attachments/assets/13bdbf62-f56f-419e-a889-77fb82cc88cb)

Using `COUNT` & `DISTINCT` to look for duplicate values in the ID column
```sql
SELECT
  COUNT(*)-COUNT(DISTINCT(id)) as' N° of Duplicate values'
FROM HC
```
This will be the result: no duplicates ID values

![Screenshot 2025-05-22 121207](https://github.com/user-attachments/assets/d1e58b5f-374d-4231-b732-e84cefd67e6a)
