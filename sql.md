SQL Interview & Practice Guide: Data Integrity (PK & FK)
Absolutely! Below is a comprehensive **SQL Interview & Practice Guide** with **50 questions and answers** focused on **verifying data integrity using Primary Key (PK) and Foreign Key (FK) constraints**. I’ve structured it for both practical and conceptual understanding.

---

## **SQL Interview & Practice Guide: Data Integrity (PK & FK)**
---

✅ These 50 Q&A cover **conceptual understanding, syntax, verification methods, testing, and scenarios** to prepare for SQL interviews and practical exercises on **data integrity via PK/FK constraints**.

---
### **Basic Concepts**

1. **Q:** What is a primary key in SQL?
   **A:** A primary key is a column (or combination of columns) that uniquely identifies each row in a table. It cannot contain NULLs and must be unique.

2. **Q:** What is a foreign key in SQL?
   **A:** A foreign key is a column (or combination of columns) in one table that refers to the primary key in another table, enforcing referential integrity.
Absolutely! Here's a simple example of two tables demonstrating **Primary Key (PK) and Foreign Key (FK)**, including some sample data.

---

### **Table 1: Departments (Parent Table)**

| DepartmentID (PK) | DepartmentName |
| ----------------- | -------------- |
| 1                 | HR             |
| 2                 | IT             |
| 3                 | Sales          |

* **Primary Key:** `DepartmentID`
* Each department has a unique `DepartmentID`.

---

### **Table 2: Employees (Child Table)**

| EmployeeID (PK) | FirstName | LastName | DepartmentID (FK) |
| --------------- | --------- | -------- | ----------------- |
| 101             | Ahmed     | Ali      | 1                 |
| 102             | Sara      | Omar     | 2                 |
| 103             | John      | Smith    | 2                 |
| 104             | Mona      | Youssef  | 3                 |

* **Primary Key:** `EmployeeID` (unique for each employee)
* **Foreign Key:** `DepartmentID` references `Departments.DepartmentID`
* This ensures that each employee is assigned to a **valid department**.


3. **Q:** Can a primary key contain NULL values?
   **A:** No, a primary key column cannot contain NULL values.

4. **Q:** Can a foreign key contain NULL values?
   **A:** Yes, unless the column is explicitly defined as NOT NULL.

5. **Q:** What is referential integrity?
   **A:** Referential integrity ensures that a foreign key value always points to an existing row in the parent table.

6. **Q:** What happens if you try to insert a duplicate value into a primary key column?
   **A:** SQL will reject the insertion and throw a primary key violation error.

7. **Q:** What happens if you try to insert a value into a foreign key column that does not exist in the parent table?
   **A:** SQL will reject the insertion and throw a foreign key violation error.

8. **Q:** Can a table have more than one primary key?
   **A:** No, but it can have a **composite primary key** (multiple columns together).

9. **Q:** Can a table have more than one foreign key?
   **A:** Yes, a table can have multiple foreign keys referencing one or more parent tables.

10. **Q:** Why are primary keys important for data integrity?
    **A:** They uniquely identify rows, prevent duplicates, and enforce entity integrity.

---

### **SQL Syntax & Verification**

11. **Q:** How do you define a primary key when creating a table?
    **A:**

    ```sql
    CREATE TABLE Employees (
        EmployeeID INT PRIMARY KEY,
        Name VARCHAR(50)
    );
    ```

12. **Q:** How do you define a foreign key when creating a table?
    **A:**

    ```sql
    CREATE TABLE Orders (
        OrderID INT PRIMARY KEY,
        EmployeeID INT,
        FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
    );
    ```

13. **Q:** How do you add a primary key to an existing table?
    **A:**

    ```sql
    ALTER TABLE Employees
    ADD CONSTRAINT PK_EmployeeID PRIMARY KEY (EmployeeID);
    ```
Sure! Let me explain your SQL statement step by step.

---


**Description:**

1. **`ALTER TABLE Employees`**

   * This command **modifies the structure** of an existing table named `Employees`.
   * You use `ALTER TABLE` to add, modify, or delete columns or constraints.

2. **`ADD CONSTRAINT PK_EmployeeID`**

   * `ADD CONSTRAINT` tells SQL that you want to **add a new rule/constraint** to the table.
   * `PK_EmployeeID` is the **name of the constraint** (you can choose any valid name).
   * Naming a constraint is helpful for **reference in error messages or if you need to drop it later**.

3. **`PRIMARY KEY (EmployeeID)`**

   * This defines the **Primary Key** on the column `EmployeeID`.
   * It ensures that:

     * `EmployeeID` values are **unique** across the table.
     * `EmployeeID` **cannot be NULL**.

---

14. **Q:** How do you add a foreign key to an existing table?
    **A:**

    ```sql
    ALTER TABLE Orders
    ADD CONSTRAINT FK_EmployeeID FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID);
    ```

15. **Q:** How do you drop a primary key from a table?
    **A:**

    ```sql
    ALTER TABLE Employees
    DROP CONSTRAINT PK_EmployeeID;
    ```

16. **Q:** How do you drop a foreign key from a table?
    **A:**

    ```sql
    ALTER TABLE Orders
    DROP CONSTRAINT FK_EmployeeID;
    ```

17. **Q:** How do you verify primary key constraints on a table?
    **A:** Query the system catalog:

    ```sql
    -- For SQL Server
    SELECT * FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS
    WHERE CONSTRAINT_TYPE = 'PRIMARY KEY' AND TABLE_NAME = 'Employees';
    ```

18. **Q:** How do you verify foreign key constraints on a table?
    **A:**

    ```sql
    -- For SQL Server
    SELECT * FROM INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS
    WHERE CONSTRAINT_NAME = 'FK_EmployeeID';
    ```

19. **Q:** How can you check which columns are part of a primary key?
    **A:**

    ```sql
    SELECT COLUMN_NAME
    FROM INFORMATION_SCHEMA.KEY_COLUMN_USAGE
    WHERE OBJECTPROPERTY(OBJECT_ID(CONSTRAINT_NAME), 'IsPrimaryKey') = 1;
    ```

20. **Q:** How can you check which columns are part of a foreign key?
    **A:**

    ```sql
    SELECT COLUMN_NAME
    FROM INFORMATION_SCHEMA.KEY_COLUMN_USAGE
    WHERE OBJECTPROPERTY(OBJECT_ID(CONSTRAINT_NAME), 'IsForeignKey') = 1;
    ```

---

### **Data Integrity Testing Questions**

21. **Q:** How do you test if the primary key constraint is enforced?
    **A:** Try inserting duplicate values into the primary key column; it should fail.

22. **Q:** How do you test if the foreign key constraint is enforced?
    **A:** Try inserting a value in the foreign key column that does not exist in the parent table; it should fail.

23. **Q:** How do you test cascading deletes?
    **A:** Create a foreign key with `ON DELETE CASCADE` and delete a row in the parent table. Rows in the child table should be deleted automatically.

24. **Q:** How do you test cascading updates?
    **A:** Create a foreign key with `ON UPDATE CASCADE` and update the primary key in the parent table. The child table should reflect the change.

25. **Q:** How do you find orphan records violating foreign key relationships?
    **A:**

## Step 1️⃣ Understand the problem (very important)

You have **two tables**:

### Parent table (main table)

Example: `Customers`

```sql
CustomerID   (Primary Key)
```

### Child table (dependent table)

Example: `Orders`

```sql
OrderID
CustomerID   (Foreign Key)
```

👉 **Orphan record** means:

* An order has a `CustomerID`
* But this `CustomerID` **does NOT exist** in the `Customers` table



## Step 2️⃣ Know what we want to find

We want to find:

> Orders that refer to customers that are not in the Customers table



## Step 3️⃣ Use LEFT JOIN (easiest way for beginners)

This is the **simplest and safest method**.

```sql
SELECT o.*
FROM Orders o
LEFT JOIN Customers c
    ON o.CustomerID = c.CustomerID
WHERE c.CustomerID IS NULL;
```



## Step 4️⃣ Understand this query line by line

### 🔹 `SELECT o.*`

* Show all columns from `Orders`



### 🔹 `FROM Orders o`

* `Orders` is the **child table**
* `o` is just a short name (alias)



### 🔹 `LEFT JOIN Customers c`

* Bring data from `Customers`
* **LEFT JOIN keeps all Orders**, even if no customer exists



### 🔹 `ON o.CustomerID = c.CustomerID`

* Match orders with customers using `CustomerID`



### 🔹 `WHERE c.CustomerID IS NULL`

* If customer data is `NULL`
* That means **no matching customer was found**
* ✅ This order is an **orphan record**



## Step 5️⃣ Simple visual example

### Customers table

| CustomerID |
| ---------- |
| 1          |
| 2          |

### Orders table

| OrderID | CustomerID |
| ------- | ---------- |
| 101     | 1          |
| 102     | 3 ❌        |

### Result of the query

| OrderID | CustomerID |
| ------- | ---------- |
| 102     | 3          |

👉 Order `102` is an orphan because **CustomerID = 3 does not exist**


## Step 6️⃣ Why this happens in real projects

* Foreign key constraint **was not added**
* Old data before constraint was created
* Manual data insertion
* Data migration issues


## Step 7️⃣ Junior-level interview answer 🧠

> To find orphan records, I use a LEFT JOIN between the child table and the parent table and check where the parent key is NULL. This shows records that don’t have a matching parent record.



## Step 8️⃣ Bonus: Easy alternative (optional)

```sql
SELECT *
FROM Orders
WHERE CustomerID NOT IN (
    SELECT CustomerID FROM Customers
);
```
---

27. **Q:** How do you check for duplicate values in a primary key column?
    **A:**

    ```sql
    SELECT EmployeeID, COUNT(*) 
    FROM Employees
    GROUP BY EmployeeID
    HAVING COUNT(*) > 1;
    ```

28. **Q:** How do you check for invalid foreign key references?
    **A:**
---

## **Tables**

### Employees

| EmployeeID | Name    |
| ---------- | ------- |
| 1          | Alice   |
| 2          | Bob     |
| 3          | Charlie |

### Orders

| OrderID | EmployeeID | Amount |
| ------- | ---------- | ------ |
| 101     | 1          | 500    |
| 102     | 3          | 250    |
| 103     | 4          | 400    |
| 104     | NULL       | 300    |

> `Orders.EmployeeID` is a foreign key reference to `Employees.EmployeeID` (but let’s assume FK constraint is **not enforced**, so invalid data can exist).

---

## **Query**

``` 
SELECT * 
FROM Orders o
WHERE NOT EXISTS (
    SELECT 1 
    FROM Employees e
    WHERE e.EmployeeID = o.EmployeeID
);

```
## **Step 2: Final Output**

| OrderID | EmployeeID | Amount |
| ------- | ---------- | ------ |
| 103     | 4          | 400    |
| 104     | NULL       | 300    |

✅ This is exactly what the query returns: all **orphan orders** (EmployeeID does not exist in Employees).



## **Different Conditions**

| Condition                | Example                | Output Explanation                                           |
| ------------------------ | ---------------------- | ------------------------------------------------------------ |
| All EmployeeIDs valid    | Orders: 101(1), 102(2) | Output: **empty** → no orphan records                        |
| Some EmployeeIDs invalid | Orders: 101(1), 103(4) | Output: 103 → only invalid EmployeeID                        |
| EmployeeID NULL          | Orders: 104(NULL)      | Output: 104 → NULL treated as invalid (no matching employee) |
| Multiple invalid         | Orders: 103(4), 105(5) | Output: 103, 105 → all invalid EmployeeIDs                   |



### ✅ Key Notes

1. `NOT EXISTS` **handles NULL safely** → includes rows where `EmployeeID` is NULL.
2. Only rows **without a matching parent** are returned.
3. If `Orders.EmployeeID` had a **proper FK constraint**, this query would **always return 0 rows**.

---

 

29. **Q:** How can you enforce NOT NULL constraint for foreign keys?
    **A:** Define the column as `NOT NULL` when creating the table:

    ```sql
    EmployeeID INT NOT NULL REFERENCES Employees(EmployeeID)
    ```

30. **Q:** Can a table have a foreign key pointing to itself?
    **A:** Yes, it’s called a self-referencing foreign key (useful for hierarchical data).

31. **Q:** How do you verify a self-referencing foreign key?
    **A:** Use:

    ```sql
    SELECT * FROM INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS
    WHERE UNIQUE_CONSTRAINT_NAME = 'PK_EmployeeID';
    ```

---

### **Advanced Verification Questions**

31. **Q:** How do you check if all foreign key constraints in the database are valid?
    **A:**

    ```sql
    SELECT OBJECT_NAME(f.parent_object_id) AS ChildTable,
           COL_NAME(fc.parent_object_id,fc.parent_column_id) AS FKColumn,
           OBJECT_NAME(f.referenced_object_id) AS ParentTable
    FROM sys.foreign_keys AS f
    INNER JOIN sys.foreign_key_columns AS fc
    ON f.object_id = fc.constraint_object_id;
    ```

32. **Q:** How do you verify primary key constraints in MySQL?
    **A:**

    ```sql
    SHOW KEYS FROM Employees WHERE Key_name = 'PRIMARY';
    ```

33. **Q:** How do you verify foreign key constraints in MySQL?
    **A:**

    ```sql
    SELECT * 
    FROM INFORMATION_SCHEMA.KEY_COLUMN_USAGE 
    WHERE TABLE_NAME = 'Orders' AND REFERENCED_TABLE_NAME IS NOT NULL;
    ```

34. **Q:** How do you enforce unique values on a column without using a primary key?
    **A:** Use a `UNIQUE` constraint:

    ```sql
    ALTER TABLE Employees ADD CONSTRAINT UQ_Email UNIQUE (Email);
    ```

35. **Q:** How do you enforce multiple-column primary keys?
    **A:**

    ```sql
    CREATE TABLE EmployeeProjects (
        EmployeeID INT,
        ProjectID INT,
        PRIMARY KEY (EmployeeID, ProjectID)
    );
    ```

36. **Q:** How do you enforce multiple-column foreign keys?
    **A:**

    ```sql
    ALTER TABLE EmployeeProjects
    ADD CONSTRAINT FK_EmployeeProject
    FOREIGN KEY (EmployeeID, ProjectID) REFERENCES Projects(EmployeeID, ProjectID);
    ```

37. **Q:** How do you check if a column has a NOT NULL constraint?
    **A:**

    ```sql
    SELECT COLUMN_NAME, IS_NULLABLE 
    FROM INFORMATION_SCHEMA.COLUMNS
    WHERE TABLE_NAME = 'Employees';
    ```

38. **Q:** How do you handle violations of foreign key constraints during bulk insert?
    **A:** Insert parent table data first, then child table data.

39. **Q:** How do you temporarily disable a foreign key constraint?
    **A:**

    ```sql
    ALTER TABLE Orders NOCHECK CONSTRAINT FK_EmployeeID;
    ```

40. **Q:** How do you re-enable a foreign key constraint after disabling?
    **A:**

    ```sql
    ALTER TABLE Orders CHECK CONSTRAINT FK_EmployeeID;
    ```

---

### **Scenario-Based Questions**

41. **Q:** A table has duplicate primary key values. How do you fix it?
    **A:** Identify duplicates using `GROUP BY` and remove duplicates while keeping one row.

42. **Q:** A foreign key column has orphan values. How do you fix it?
    **A:** Either delete orphan rows or insert matching rows in the parent table.

43. **Q:** You need to create a hierarchical employee table. How do you enforce manager-subordinate relationships?
    **A:** Create a self-referencing foreign key:

    ```sql
    ALTER TABLE Employees
    ADD CONSTRAINT FK_Manager FOREIGN KEY (ManagerID) REFERENCES Employees(EmployeeID);
    ```

44. **Q:** How can you ensure cascading delete does not violate business rules?
    **A:** Use `ON DELETE NO ACTION` or `ON DELETE RESTRICT` to prevent accidental deletion.

45. **Q:** How do you check which child tables are linked to a parent table?
    **A:**

    ```sql
    SELECT * 
    FROM INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS
    WHERE UNIQUE_CONSTRAINT_NAME = 'PK_EmployeeID';
    ```

46. **Q:** How do you check data integrity for multiple tables at once?
    **A:** Write queries joining child and parent tables to ensure all foreign key values exist in parent tables.

47. **Q:** How do you verify that all primary key values are unique across partitions?
    **A:** Use `GROUP BY` with `HAVING COUNT(*) > 1` across partitions.

48. **Q:** How can you test cascading updates for multiple foreign keys?
    **A:** Create multiple foreign key relationships with `ON UPDATE CASCADE` and update the parent table.

49. **Q:** How do you test if foreign key constraints prevent deletion when `ON DELETE RESTRICT` is used?
    **A:** Attempt to delete a parent row; it should fail if child rows exist.

50. **Q:** How can you generate a report of all primary and foreign key constraints in the database?
    **A:**

    ```sql
    SELECT tc.TABLE_NAME, tc.CONSTRAINT_NAME, tc.CONSTRAINT_TYPE
    FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS tc
    WHERE tc.CONSTRAINT_TYPE IN ('PRIMARY KEY','FOREIGN KEY');
    ```

---

✅ These 50 Q&A cover **all CRUD operations, verification techniques, transactions, safeguards, and practical scenarios** to prepare for SQL interviews and hands-on database testing.

---

## **SQL Interview & Practice Guide: Verify CRUD Operations**

### **Basic Concepts**

1. **Q:** What does CRUD stand for?
   **A:** CRUD stands for **Create, Read, Update, Delete**, the four basic operations on database records.

2. **Q:** Which SQL statement is used to create a new record?
   **A:** `INSERT INTO` statement.

3. **Q:** Which SQL statement is used to read data from a table?
   **A:** `SELECT` statement.

4. **Q:** Which SQL statement is used to update existing records?
   **A:** `UPDATE` statement.

5. **Q:** Which SQL statement is used to delete records?
   **A:** `DELETE FROM` statement.

6. **Q:** Can you insert multiple rows in a single SQL query?
   **A:** Yes, using multiple `VALUES` clauses:

   ```sql
   INSERT INTO Employees (EmployeeID, Name) VALUES 
   (1, 'Alice'),
   (2, 'Bob');
   ```

7. **Q:** How do you select all columns from a table?
   **A:**

   ```sql
   SELECT * FROM Employees;
   ```

8. **Q:** How do you select specific columns from a table?
   **A:**

   ```sql
   SELECT EmployeeID, Name FROM Employees;
   ```

9. **Q:** How do you select distinct values in a column?
   **A:**

   ```sql
   SELECT DISTINCT Department FROM Employees;
   ```
Sure! Let’s break it down.

---

### **SQL Statement:**

```sql
SELECT DISTINCT Department FROM Employees;
```

---

 **Meaning:**

2. **`DISTINCT`**

   * Ensures that **only unique values** are returned.
   * If a column has duplicate values, `DISTINCT` **removes duplicates**.
---

### **Effect:**

* Returns a **list of all unique departments** from the `Employees` table.
* Duplicate department names are **shown only once**.

---

### **Example:**

**Employees Table:**

| EmployeeID | FirstName | Department |
| ---------- | --------- | ---------- |
| 101        | Ahmed     | HR         |
| 102        | Sara      | IT         |
| 103        | John      | IT         |
| 104        | Mona      | Sales      |
| 105        | Ali       | HR         |

**Query Result:**

| Department |
| ---------- |
| HR         |
| IT         |
| Sales      |

---

✅ **Key Point:**

* `DISTINCT` is very useful when you want to **list unique values** in a column or combination of columns.

---


10. **Q:** How do you filter records based on a condition?
    **A:** Using `WHERE` clause:

    ```sql
    SELECT * FROM Employees WHERE Department = 'HR';
    ```

---

### **Create Operation (INSERT)**

11. **Q:** How do you insert a single row into a table?
    **A:**

    ```sql
    INSERT INTO Employees (EmployeeID, Name, Department) VALUES (1, 'Alice', 'HR');
    ```

12. **Q:** How do you insert data into all columns without specifying column names?
    **A:**

    ```sql
    INSERT INTO Employees VALUES (2, 'Bob', 'IT');
    ```

13. **Q:** What happens if you insert a NULL into a NOT NULL column?
    **A:** SQL will throw a constraint violation error.

14. **Q:** How do you insert data using a `SELECT` from another table?
    **A:**

    ```sql
    INSERT INTO EmployeesBackup (EmployeeID, Name, Department)
    SELECT EmployeeID, Name, Department FROM Employees;
    ```

15. **Q:** How do you verify that an `INSERT` operation was successful?
    **A:** Use a `SELECT` query:

    ```sql
    SELECT * FROM Employees WHERE EmployeeID = 1;
    ```

16. **Q:** How do you handle duplicate primary key values during insert?
    **A:** SQL will reject the insert. Use `ON DUPLICATE KEY UPDATE` in MySQL or `MERGE` in SQL Server.

17. **Q:** How do you insert multiple rows efficiently?
    **A:**

    ```sql
    INSERT INTO Employees (EmployeeID, Name) VALUES (3, 'Charlie'), (4, 'David');
    ```

18. **Q:** How do you insert default values for certain columns?
    **A:**

    ```sql
    INSERT INTO Employees (EmployeeID, Name) VALUES (5, 'Eve');
    ```

19. **Q:** How do you check auto-increment values after insert?
    **A:**

    ```sql
    SELECT LAST_INSERT_ID(); -- MySQL
    SELECT SCOPE_IDENTITY(); -- SQL Server
    ```

20. **Q:** How do you insert a row but avoid inserting duplicates?
    **A:** Use `INSERT IGNORE` (MySQL) or `MERGE` (SQL Server).

---

### **Read Operation (SELECT)**

21. **Q:** How do you read all rows from a table?
    **A:**

    ```sql
    SELECT * FROM Employees;
    ```

22. **Q:** How do you read rows with specific conditions?
    **A:**

    ```sql
    SELECT * FROM Employees WHERE Department = 'IT';
    ```

23. **Q:** How do you read rows sorted by a column?
    **A:**

    ```sql
    SELECT * FROM Employees ORDER BY Name ASC;
    ```

24. **Q:** How do you read top N rows?
    **A:**

    ```sql
    SELECT TOP 5 * FROM Employees; -- SQL Server
    SELECT * FROM Employees LIMIT 5; -- MySQL
    ```

25. **Q:** How do you read rows using pattern matching?
    **A:**

    ```sql
    SELECT * FROM Employees WHERE Name LIKE 'A%';
    ```

26. **Q:** How do you read data from multiple tables?
    **A:** Use `JOIN`:

    ```sql
    SELECT e.Name, d.DepartmentName
    FROM Employees e
    JOIN Departments d ON e.Department = d.DepartmentID;
    ```

27. **Q:** How do you read aggregated data?
    **A:**

    ```sql
    SELECT Department, COUNT(*) AS EmployeeCount
    FROM Employees
    GROUP BY Department;
    ```

28. **Q:** How do you filter aggregated data?
    **A:**

    ```sql
    SELECT Department, COUNT(*) AS EmployeeCount
    FROM Employees
    GROUP BY Department
    HAVING COUNT(*) > 5;
    ```

29. **Q:** How do you read distinct combinations of multiple columns?
    **A:**

    ```sql
    SELECT DISTINCT Department, Role FROM Employees;
    ```

30. **Q:** How do you read data using subqueries?
    **A:**

    ```sql
    SELECT * FROM Employees
    WHERE Department IN (SELECT DepartmentID FROM Departments WHERE Location='NY');
    ```

---

### **Update Operation (UPDATE)**

31. **Q:** How do you update a single row?
    **A:**

    ```sql
    UPDATE Employees SET Department='Finance' WHERE EmployeeID=1;
    ```

32. **Q:** How do you update multiple rows?
    **A:**

    ```sql
    UPDATE Employees SET Department='HR' WHERE Department='Human Resources';
    ```

33. **Q:** How do you update based on a join with another table?
    **A:**

    ```sql
    UPDATE e
    SET e.Department = d.NewDepartment
    FROM Employees e
    JOIN DepartmentChanges d ON e.EmployeeID = d.EmployeeID;
    ```

34. **Q:** How do you prevent accidental updates to all rows?
    **A:** Always include a `WHERE` clause.

35. **Q:** How do you verify an update operation?
    **A:**

    ```sql
    SELECT * FROM Employees WHERE EmployeeID=1;
    ```

36. **Q:** How do you update a column using values from another column in the same table?
    **A:**

    ```sql
    UPDATE Employees SET Department = PreviousDepartment;
    ```

37. **Q:** How do you increment a numeric column?
    **A:**

    ```sql
    UPDATE Employees SET Salary = Salary + 1000 WHERE Department='IT';
    ```

38. **Q:** How do you update multiple columns at once?
    **A:**

    ```sql
    UPDATE Employees SET Department='IT', Salary=5000 WHERE EmployeeID=2;
    ```

39. **Q:** How do you rollback an update if something goes wrong?
    **A:** Use transactions:

    ```sql
    BEGIN TRANSACTION;
    UPDATE Employees SET Salary=6000 WHERE EmployeeID=3;
    ROLLBACK; -- or COMMIT;
    ```

40. **Q:** How do you update rows conditionally using CASE?
    **A:**

    ```sql
    UPDATE Employees
    SET Department = CASE WHEN Department='IT' THEN 'Tech' ELSE Department END;
    ```

---

### **Delete Operation (DELETE)**

41. **Q:** How do you delete a single row?
    **A:**

    ```sql
    DELETE FROM Employees WHERE EmployeeID=1;
    ```

42. **Q:** How do you delete multiple rows?
    **A:**

    ```sql
    DELETE FROM Employees WHERE Department='Temp';
    ```

43. **Q:** How do you delete all rows without dropping the table?
    **A:**

    ```sql
    DELETE FROM Employees;
    ```

44. **Q:** How do you truncate a table?
    **A:**

    ```sql
    TRUNCATE TABLE Employees;
    ```

45. **Q:** What is the difference between DELETE and TRUNCATE?
    **A:** `DELETE` can have a `WHERE` clause and is logged; `TRUNCATE` removes all rows and resets identity columns.

46. **Q:** How do you verify a delete operation?
    **A:**

    ```sql
    SELECT * FROM Employees WHERE EmployeeID=1;
    ```

47. **Q:** How do you delete using a subquery?
    **A:**

    ```sql
    DELETE FROM Employees
    WHERE Department IN (SELECT DepartmentID FROM Departments WHERE Location='NY');
    ```

48. **Q:** How do you prevent accidental delete of all rows?
    **A:** Always use a `WHERE` clause; consider using transactions.

49. **Q:** How do you delete rows based on a join with another table?
    **A:**

    ```sql
    DELETE e
    FROM Employees e
    JOIN TempEmployees t ON e.EmployeeID = t.EmployeeID;
    ```

50. **Q:** How do you undo a delete operation?
    **A:** Use transactions:

    ```sql
    BEGIN TRANSACTION;
    DELETE FROM Employees WHERE EmployeeID=5;
    ROLLBACK; -- undo
    COMMIT; -- confirm
    ```


---

##✅  **50 Q&A cover conceptual understanding, syntax, testing, verification, and scenarios** for **triggers, stored procedures, and functions**.

---

---

 **SQL Interview & Practice Guide: Verify Triggers, Stored Procedures, and Functions**

---

### **Basic Concepts**

1. **Q:** What is a trigger in SQL?
   **A:** A trigger is a special kind of stored procedure that automatically executes in response to certain events on a table or view (INSERT, UPDATE, DELETE).

2. **Q:** What is a stored procedure?
   **A:** A stored procedure is a precompiled set of SQL statements stored in the database and executed as a single unit.

3. **Q:** What is a function in SQL?
   **A:** A function is a database object that returns a single value or table and can be used in SQL statements.

4. **Q:** What is the difference between a trigger and a stored procedure?
   **A:** Triggers execute automatically based on table events; stored procedures execute explicitly by calling them.

5. **Q:** Can a function modify database tables?
   **A:** In most SQL databases, functions cannot perform actions that modify tables; they are usually read-only.

6. **Q:** Can a trigger call a stored procedure?
   **A:** Yes, triggers can call stored procedures to perform complex logic.

7. **Q:** What types of triggers exist?
   **A:** `AFTER`, `BEFORE`, `INSTEAD OF` triggers.

8. **Q:** What types of functions exist in SQL?
   **A:** Scalar functions (return single value), Table-valued functions (return a table).

9. **Q:** What is the difference between inline and multi-statement table-valued functions?
   **A:** Inline functions contain a single SELECT statement; multi-statement functions can have multiple statements with table variable.

10. **Q:** What are the advantages of stored procedures?
    **A:** Precompiled execution, code reuse, reduced network traffic, centralized logic.

---

### **Creating and Verifying Stored Procedures**

11. **Q:** How do you create a simple stored procedure?
    **A:**

    ```sql
    CREATE PROCEDURE GetEmployee
    @EmployeeID INT
    AS
    SELECT * FROM Employees WHERE EmployeeID = @EmployeeID;
    ```

12. **Q:** How do you execute a stored procedure?
    **A:**

    ```sql
    EXEC GetEmployee @EmployeeID = 1;
    ```

13. **Q:** How do you alter an existing stored procedure?
    **A:**

    ```sql
    ALTER PROCEDURE GetEmployee
    @EmployeeID INT
    AS
    SELECT Name, Department FROM Employees WHERE EmployeeID=@EmployeeID;
    ```

14. **Q:** How do you drop a stored procedure?
    **A:**

    ```sql
    DROP PROCEDURE GetEmployee;
    ```

15. **Q:** How do you check if a stored procedure exists in SQL Server?
    **A:**

    ```sql
    SELECT * FROM sys.objects WHERE type='P' AND name='GetEmployee';
    ```

16. **Q:** How do you pass multiple parameters to a stored procedure?
    **A:**

    ```sql
    CREATE PROCEDURE GetEmployeeDetails
    @EmployeeID INT,
    @Department VARCHAR(50)
    AS
    SELECT * FROM Employees WHERE EmployeeID=@EmployeeID AND Department=@Department;
    ```

17. **Q:** How do you verify stored procedure execution results?
    **A:** Execute the procedure and check the returned data:

    ```sql
    EXEC GetEmployeeDetails 1, 'IT';
    ```

18. **Q:** How do you handle errors inside a stored procedure?
    **A:** Use `TRY...CATCH` blocks:

    ```sql
    BEGIN TRY
        -- SQL statements
    END TRY
    BEGIN CATCH
        PRINT ERROR_MESSAGE();
    END CATCH;
    ```

19. **Q:** How do you test stored procedures for edge cases?
    **A:** Provide boundary or invalid inputs and verify expected results or error handling.

20. **Q:** Can stored procedures return output parameters?
    **A:** Yes:

    ```sql
    CREATE PROCEDURE GetEmployeeName
    @EmployeeID INT,
    @Name VARCHAR(50) OUTPUT
    AS
    SELECT @Name = Name FROM Employees WHERE EmployeeID=@EmployeeID;
    ```

---

### **Creating and Verifying Functions**

21. **Q:** How do you create a scalar function?
    **A:**

    ```sql
    CREATE FUNCTION GetEmployeeSalary(@EmployeeID INT)
    RETURNS INT
    AS
    BEGIN
        DECLARE @Salary INT;
        SELECT @Salary = Salary FROM Employees WHERE EmployeeID=@EmployeeID;
        RETURN @Salary;
    END;
    ```

22. **Q:** How do you use a scalar function in a SELECT statement?
    **A:**

    ```sql
    SELECT Name, dbo.GetEmployeeSalary(EmployeeID) AS Salary FROM Employees;
    ```

23. **Q:** How do you create a table-valued function?
    **A:**

    ```sql
    CREATE FUNCTION GetEmployeesByDepartment(@Department VARCHAR(50))
    RETURNS TABLE
    AS
    RETURN (SELECT * FROM Employees WHERE Department=@Department);
    ```

24. **Q:** How do you query a table-valued function?
    **A:**

    ```sql
    SELECT * FROM dbo.GetEmployeesByDepartment('IT');
    ```

25. **Q:** How do you alter a function?
    **A:**

    ```sql
    ALTER FUNCTION GetEmployeeSalary(@EmployeeID INT) RETURNS INT AS ...
    ```

26. **Q:** How do you drop a function?
    **A:**

    ```sql
    DROP FUNCTION GetEmployeeSalary;
    ```

27. **Q:** How do you verify function existence?
    **A:**

    ```sql
    SELECT * FROM sys.objects WHERE type='FN' AND name='GetEmployeeSalary';
    ```

28. **Q:** Can functions contain transactions?
    **A:** No, functions are usually restricted to read-only operations.

29. **Q:** How do you test a function?
    **A:** Call the function with different input values and validate the output.

30. **Q:** How do you use a function in WHERE clause?
    **A:**

    ```sql
    SELECT * FROM Employees WHERE dbo.GetEmployeeSalary(EmployeeID) > 5000;
    ```

---

### **Creating and Verifying Triggers**

31. **Q:** How do you create an AFTER INSERT trigger?
    **A:**

    ```sql
    CREATE TRIGGER trgAfterInsertEmployee
    ON Employees
    AFTER INSERT
    AS
    BEGIN
        PRINT 'New employee added';
    END;
    ```

32. **Q:** How do you create a BEFORE UPDATE trigger?
    **A:** (MySQL example)

    ```sql
    CREATE TRIGGER trgBeforeUpdateEmployee
    BEFORE UPDATE ON Employees
    FOR EACH ROW
    SET NEW.LastModified = NOW();
    ```

33. **Q:** How do you create an INSTEAD OF DELETE trigger?
    **A:**

    ```sql
    CREATE TRIGGER trgInsteadOfDelete
    ON Employees
    INSTEAD OF DELETE
    AS
    BEGIN
        PRINT 'Delete prevented';
    END;
    ```

34. **Q:** How do you verify trigger existence?
    **A:**

    ```sql
    SELECT * FROM sys.triggers WHERE name='trgAfterInsertEmployee';
    ```

35. **Q:** How do you test a trigger?
    **A:** Perform the action (INSERT/UPDATE/DELETE) and verify trigger behavior, e.g., log table updates or printed messages.

36. **Q:** How do you disable a trigger?
    **A:**

    ```sql
    DISABLE TRIGGER trgAfterInsertEmployee ON Employees;
    ```

37. **Q:** How do you enable a trigger?
    **A:**

    ```sql
    ENABLE TRIGGER trgAfterInsertEmployee ON Employees;
    ```

38. **Q:** How do you drop a trigger?
    **A:**

    ```sql
    DROP TRIGGER trgAfterInsertEmployee;
    ```

39. **Q:** How do you view all triggers on a table?
    **A:**

    ```sql
    SELECT * FROM sys.triggers WHERE parent_id = OBJECT_ID('Employees');
    ```

40. **Q:** How do you check which events a trigger responds to?
    **A:** Query `sys.triggers` and `sys.trigger_events` (SQL Server) or use `SHOW TRIGGERS` in MySQL.

---

### **Testing and Verification Scenarios**

41. **Q:** How do you verify that a trigger correctly inserts audit records?
    **A:** Insert/update/delete a row and check the audit table for expected entries.

42. **Q:** How do you test a stored procedure with multiple output parameters?
    **A:** Call the procedure and verify the values of all output parameters.

43. **Q:** How do you test a stored procedure with transactions?
    **A:** Intentionally cause an error to see if rollback occurs as expected.

44. **Q:** How do you test a function with boundary input values?
    **A:** Call the function with min/max or invalid values and verify behavior.

45. **Q:** How do you check trigger execution order when multiple triggers exist on the same table?
    **A:** Use `sp_helptrigger Employees` (SQL Server) or `SHOW TRIGGERS` (MySQL).

46. **Q:** How do you prevent a trigger from causing infinite loops?
    **A:** Use `IF UPDATE(ColumnName)` conditions and avoid recursive updates.

47. **Q:** How do you verify error handling in stored procedures?
    **A:** Call the procedure with invalid data and check that errors are logged or handled.

48. **Q:** How do you verify that a function returns NULL for non-existent data?
    **A:** Call the function with an ID that doesn’t exist in the table.

49. **Q:** How do you check if a trigger affects performance?
    **A:** Use execution plan, profiler, or measure insert/update/delete timings before and after enabling the trigger.

50. **Q:** How do you document triggers, functions, and stored procedures for QA verification?
    **A:** Maintain a table with columns: Name, Type (Trigger/SP/Function), Table, Event, Input/Output, Purpose, Test Cases.


---

✅ This guide provides **50 join-related Q&A/exercises** with **sample table values and expected outputs**, ready for **interview prep and practical SQL verification**.

---
Great interview question 👍
I’ll show you **sample tables**, then **each join type**, and **the exact output difference** so it’s very clear.

---

## 📋 Sample Tables

### **Employees**

| EmpID | EmpName | DeptID |
| ----- | ------- | ------ |
| 1     | Ahmed   | 10     |
| 2     | Sara    | 20     |
| 3     | John    | 30     |
| 4     | Mona    | NULL   |

---

### **Departments**

| DeptID | DeptName |
| ------ | -------- |
| 10     | HR       |
| 20     | IT       |
| 40     | Finance  |

---

## 1️⃣ INNER JOIN

👉 Returns **only matching rows** from both tables.

```sql
SELECT e.EmpName, d.DeptName
FROM Employees e
INNER JOIN Departments d
ON e.DeptID = d.DeptID;
```

### Result:

| EmpName | DeptName |
| ------- | -------- |
| Ahmed   | HR       |
| Sara    | IT       |

❌ John (DeptID 30 not in Departments)
❌ Mona (NULL DeptID)

---

## 2️⃣ LEFT JOIN (LEFT OUTER JOIN)

👉 Returns **all rows from LEFT table (Employees)** + matching rows from right table.

```sql
SELECT e.EmpName, d.DeptName
FROM Employees e
LEFT JOIN Departments d
ON e.DeptID = d.DeptID;
```

### Result:

| EmpName | DeptName |
| ------- | -------- |
| Ahmed   | HR       |
| Sara    | IT       |
| John    | NULL     |
| Mona    | NULL     |

✔ All employees returned
✔ Missing department shows `NULL`

---

## 3️⃣ RIGHT JOIN (RIGHT OUTER JOIN)

👉 Returns **all rows from RIGHT table (Departments)** + matching rows from left table.

```sql
SELECT e.EmpName, d.DeptName
FROM Employees e
RIGHT JOIN Departments d
ON e.DeptID = d.DeptID;
```

### Result:

| EmpName | DeptName |
| ------- | -------- |
| Ahmed   | HR       |
| Sara    | IT       |
| NULL    | Finance  |

✔ All departments returned
✔ Finance has no employees → `NULL`

---

## 4️⃣ FULL OUTER JOIN

👉 Returns **all rows from both tables**, matched where possible.

```sql
SELECT e.EmpName, d.DeptName
FROM Employees e
FULL OUTER JOIN Departments d
ON e.DeptID = d.DeptID;
```

### Result:

| EmpName | DeptName |
| ------- | -------- |
| Ahmed   | HR       |
| Sara    | IT       |
| John    | NULL     |
| Mona    | NULL     |
| NULL    | Finance  |

✔ Shows **everything**
✔ Unmatched rows filled with `NULL`

---

## 5️⃣ SELF JOIN

👉 Join a table **with itself**
Example: Employees & their Managers

### Employees Table (example)

| EmpID | EmpName | ManagerID |
| ----- | ------- | --------- |
| 1     | Ahmed   | NULL      |
| 2     | Sara    | 1         |
| 3     | John    | 1         |

```sql
SELECT e.EmpName AS Employee, m.EmpName AS Manager
FROM Employees e
LEFT JOIN Employees m
ON e.ManagerID = m.EmpID;
```

### Result:

| Employee | Manager |
| -------- | ------- |
| Ahmed    | NULL    |
| Sara     | Ahmed   |
| John     | Ahmed   |

---

## 🧠 Interview Summary (VERY IMPORTANT)

| Join Type  | Returns                   |
| ---------- | ------------------------- |
| INNER JOIN | Only matching rows        |
| LEFT JOIN  | All left table rows       |
| RIGHT JOIN | All right table rows      |
| FULL JOIN  | All rows from both tables |
| SELF JOIN  | Table joined to itself    |

---

---

## **SQL Interview & Practice Guide: Joins with Table Values and Output Verification**

### **Sample Tables**

**Employees Table**

| EmployeeID | Name    | DepartmentID |
| ---------- | ------- | ------------ |
| 1          | Alice   | 10           |
| 2          | Bob     | 20           |
| 3          | Charlie | 10           |
| 4          | David   | 30           |
| 5          | Eve     | 20           |

**Departments Table**

| DepartmentID | DepartmentName |
| ------------ | -------------- |
| 10           | HR             |
| 20           | IT             |
| 30           | Finance        |
| 40           | Marketing      |

---

### **Basic Join Questions**

1. **Q:** What is an INNER JOIN?
   **A:** Returns only matching rows between two tables.

   ```sql
   SELECT e.Name, d.DepartmentName
   FROM Employees e
   INNER JOIN Departments d
   ON e.DepartmentID = d.DepartmentID;
   ```

   **Output:**

   | Name    | DepartmentName |
   | ------- | -------------- |
   | Alice   | HR             |
   | Bob     | IT             |
   | Charlie | HR             |
   | David   | Finance        |
   | Eve     | IT             |

2. **Q:** What is a LEFT JOIN?
   **A:** Returns all rows from the left table, with NULLs for non-matching rows from the right table.

   ```sql
   SELECT e.Name, d.DepartmentName
   FROM Employees e
   LEFT JOIN Departments d
   ON e.DepartmentID = d.DepartmentID;
   ```

   **Output:** Same as INNER JOIN here, all employees have departments, but if Employee had DepartmentID=50, it would show NULL.

3. **Q:** What is a RIGHT JOIN?
   **A:** Returns all rows from the right table, with NULLs for non-matching rows from the left table.

   ```sql
   SELECT e.Name, d.DepartmentName
   FROM Employees e
   RIGHT JOIN Departments d
   ON e.DepartmentID = d.DepartmentID;
   ```

   **Output:**

   | Name    | DepartmentName |
   | ------- | -------------- |
   | Alice   | HR             |
   | Bob     | IT             |
   | Charlie | HR             |
   | David   | Finance        |
   | Eve     | IT             |
   | NULL    | Marketing      |

4. **Q:** What is a FULL OUTER JOIN?
   **A:** Returns all rows from both tables, with NULLs where there’s no match.

   ```sql
   SELECT e.Name, d.DepartmentName
   FROM Employees e
   FULL OUTER JOIN Departments d
   ON e.DepartmentID = d.DepartmentID;
   ```

   **Output:**

   | Name    | DepartmentName |
   | ------- | -------------- |
   | Alice   | HR             |
   | Bob     | IT             |
   | Charlie | HR             |
   | David   | Finance        |
   | Eve     | IT             |
   | NULL    | Marketing      |

5. **Q:** How do you perform a CROSS JOIN?
   **A:** Returns all combinations of rows from both tables.

   ```sql
   SELECT e.Name, d.DepartmentName
   FROM Employees e
   CROSS JOIN Departments d;
   ```

   **Output:** 5 employees × 4 departments = 20 rows.

---

### **Join with WHERE Clauses**

6. **Q:** How do you filter INNER JOIN results?

```sql
SELECT e.Name, d.DepartmentName
FROM Employees e
INNER JOIN Departments d
ON e.DepartmentID = d.DepartmentID
WHERE d.DepartmentName='IT';
```

**Output:**

| Name | DepartmentName |
| ---- | -------------- |
| Bob  | IT             |
| Eve  | IT             |

7. **Q:** How do you use LEFT JOIN with WHERE condition on the right table?

```sql
SELECT e.Name, d.DepartmentName
FROM Employees e
LEFT JOIN Departments d
ON e.DepartmentID = d.DepartmentID
WHERE d.DepartmentName='Marketing';
```

**Output:**

| Name | DepartmentName |
| ---- | -------------- |
| NULL | Marketing      |

---

### **Self Joins**

8. **Q:** What is a self join?
   **A:** Joining a table with itself.

**Sample Data:** Employees table has ManagerID

| EmployeeID | Name    | ManagerID |
| ---------- | ------- | --------- |
| 1          | Alice   | NULL      |
| 2          | Bob     | 1         |
| 3          | Charlie | 1         |
| 4          | David   | 2         |

**Query:** Find employee and their manager.

```sql
SELECT e.Name AS Employee, m.Name AS Manager
FROM Employees e
LEFT JOIN Employees m
ON e.ManagerID = m.EmployeeID;
```

**Output:**

| Employee | Manager |
| -------- | ------- |
| Alice    | NULL    |
| Bob      | Alice   |
| Charlie  | Alice   |
| David    | Bob     |

---

### **Multiple Table Joins**

9. **Q:** Join Employees, Departments, and Salaries tables.

**Salaries Table:**

| EmployeeID | Salary |
| ---------- | ------ |
| 1          | 5000   |
| 2          | 6000   |
| 3          | 5500   |
| 4          | 4500   |
| 5          | 7000   |

```sql
SELECT e.Name, d.DepartmentName, s.Salary
FROM Employees e
INNER JOIN Departments d ON e.DepartmentID = d.DepartmentID
INNER JOIN Salaries s ON e.EmployeeID = s.EmployeeID;
```

**Output:**

| Name    | DepartmentName | Salary |
| ------- | -------------- | ------ |
| Alice   | HR             | 5000   |
| Bob     | IT             | 6000   |
| Charlie | HR             | 5500   |
| David   | Finance        | 4500   |
| Eve     | IT             | 7000   |

10. **Q:** How to find employees without salaries using LEFT JOIN?

```sql
SELECT e.Name, s.Salary
FROM Employees e
LEFT JOIN Salaries s ON e.EmployeeID = s.EmployeeID
WHERE s.Salary IS NULL;
```

**Output:** If all have salaries, result is empty.

---

### **Advanced Join Queries**

11. **Q:** Find highest-paid employee per department.

```sql
SELECT d.DepartmentName, e.Name, s.Salary
FROM Employees e
JOIN Salaries s ON e.EmployeeID = s.EmployeeID
JOIN Departments d ON e.DepartmentID = d.DepartmentID
WHERE s.Salary = (SELECT MAX(Salary)
                  FROM Salaries s2
                  JOIN Employees e2 ON s2.EmployeeID = e2.EmployeeID
                  WHERE e2.DepartmentID = e.DepartmentID);
```

**Output:**

| DepartmentName | Name    | Salary |
| -------------- | ------- | ------ |
| HR             | Charlie | 5500   |
| IT             | Eve     | 7000   |
| Finance        | David   | 4500   |

12. **Q:** Find employees not assigned to any department.

```sql
SELECT e.Name
FROM Employees e
LEFT JOIN Departments d ON e.DepartmentID = d.DepartmentID
WHERE d.DepartmentID IS NULL;
```

**Output:** Empty (based on sample data).

---

### **Questions 13-50 (Examples & Exercises)**

You can create exercises by combining:

* **INNER, LEFT, RIGHT, FULL, CROSS JOIN**
* **Multiple table joins** (Employees, Departments, Salaries, Projects)
* **Self joins** (Manager-Employee)
* **Join with aggregates** (SUM, MAX, COUNT per department)
* **Join with WHERE, GROUP BY, HAVING**
* **Detect missing data** with LEFT JOIN + `IS NULL`

**Examples of exercises:**

13. Find employees in department 'HR'.
14. List employees with salary > 6000.
15. Count employees per department.
16. List departments without employees.
17. List employees with their project names.
18. Find employees earning above average salary.
19. Join Employees and Departments to list all employees including unmatched departments.
20. Self join to find peer employees in the same department.
21. Join three tables: Employees, Projects, Salaries.
22. Find departments with max number of employees.
23. Join and order employees by salary descending.
24. Join Employees with Managers (self join).
25. Cross join Employees with Departments.
26. Find employees who do not have salary entry.
27. Join with CASE statements to classify salaries.
28. Join Employees and Departments filtering specific departments.
29. List employees and project counts per employee.
30. Find employees with multiple department assignments.
31. Join Employees and Salaries for employees with salary > 5000.
32. Find second highest salary per department using join.
33. Join Employees and Departments for employees hired in 2025.
34. Join Employees and Salaries, calculate bonus as 10% of salary.
35. Find employees without projects using LEFT JOIN.
36. List employees with their department and project names.
37. Join to find employees sharing same manager.
38. Find employees whose salary is below department average.
39. Join tables to detect duplicate assignments.
40. List all employees and salaries using FULL OUTER JOIN.
41. Self join to find employees reporting to same manager.
42. Join Employees, Departments, Salaries to find top 3 salaries per department.
43. Join tables to find employees not assigned any projects.
44. Use join with GROUP BY to find total salary per department.
45. Join Employees and Departments for department head details.
46. Join with aggregate to find min/max salary per department.
47. Join Employees and Projects with project status filter.
48. Find employees working in multiple departments using join.
49. Use join with HAVING to filter departments with >2 employees.
50. Cross join Employees and Departments to create assignment test matrix.



If you want, I can create a **full SQL interview mega guide** with **200+ Q&A**, combining **CRUD, Joins, Data Integrity, Triggers, SPs, Functions, Views, and Advanced SQL**, **all with sample data and verification outputs**.

Do you want me to do that?
Perfect! Let’s go **step by step** and provide **answers with actual SQL queries, sample outputs, and verification** for the **50 join questions/exercises** mentioned in the previous guide. I’ll use the **sample tables**:

---

### **Sample Tables for Reference**

**Employees**

| EmployeeID | Name    | DepartmentID | ManagerID |
| ---------- | ------- | ------------ | --------- |
| 1          | Alice   | 10           | NULL      |
| 2          | Bob     | 20           | 1         |
| 3          | Charlie | 10           | 1         |
| 4          | David   | 30           | 2         |
| 5          | Eve     | 20           | 2         |

**Departments**

| DepartmentID | DepartmentName |
| ------------ | -------------- |
| 10           | HR             |
| 20           | IT             |
| 30           | Finance        |
| 40           | Marketing      |

**Salaries**

| EmployeeID | Salary |
| ---------- | ------ |
| 1          | 5000   |
| 2          | 6000   |
| 3          | 5500   |
| 4          | 4500   |
| 5          | 7000   |

**Projects**

| ProjectID | ProjectName | EmployeeID |
| --------- | ----------- | ---------- |
| 101       | Alpha       | 1          |
| 102       | Beta        | 2          |
| 103       | Gamma       | 3          |
| 104       | Delta       | 5          |

---

### **Answers with Queries and Outputs**

---

**1. Employees in department 'HR'**

```sql
SELECT e.Name, d.DepartmentName
FROM Employees e
JOIN Departments d ON e.DepartmentID = d.DepartmentID
WHERE d.DepartmentName='HR';
```

**Output:**

| Name    | DepartmentName |
| ------- | -------------- |
| Alice   | HR             |
| Charlie | HR             |

---

**2. Employees with salary > 6000**

```sql
SELECT e.Name, s.Salary
FROM Employees e
JOIN Salaries s ON e.EmployeeID = s.EmployeeID
WHERE s.Salary > 6000;
```

**Output:**

| Name | Salary |
| ---- | ------ |
| Eve  | 7000   |

---

**3. Count employees per department**

```sql
SELECT d.DepartmentName, COUNT(e.EmployeeID) AS EmployeeCount
FROM Departments d
LEFT JOIN Employees e ON d.DepartmentID = e.DepartmentID
GROUP BY d.DepartmentName;
```

**Output:**

| DepartmentName | EmployeeCount |
| -------------- | ------------- |
| HR             | 2             |
| IT             | 2             |
| Finance        | 1             |
| Marketing      | 0             |

---

**4. Departments without employees**

```sql
SELECT d.DepartmentName
FROM Departments d
LEFT JOIN Employees e ON d.DepartmentID = e.DepartmentID
WHERE e.EmployeeID IS NULL;
```

**Output:**

| DepartmentName |
| -------------- |
| Marketing      |

---

**5. Employees with their project names**

```sql
SELECT e.Name, p.ProjectName
FROM Employees e
LEFT JOIN Projects p ON e.EmployeeID = p.EmployeeID;
```

**Output:**

| Name    | ProjectName |
| ------- | ----------- |
| Alice   | Alpha       |
| Bob     | Beta        |
| Charlie | Gamma       |
| David   | NULL        |
| Eve     | Delta       |

---

**6. Employees earning above average salary**

```sql
SELECT e.Name, s.Salary
FROM Employees e
JOIN Salaries s ON e.EmployeeID = s.EmployeeID
WHERE s.Salary > (SELECT AVG(Salary) FROM Salaries);
```

**Output:** Average salary = (5000+6000+5500+4500+7000)/5 = 5600

| Name | Salary |
| ---- | ------ |
| Bob  | 6000   |
| Eve  | 7000   |

---

**7. Employees including unmatched departments**

```sql
SELECT e.Name, d.DepartmentName
FROM Employees e
LEFT JOIN Departments d ON e.DepartmentID = d.DepartmentID;
```

**Output:** All employees have departments, same as INNER JOIN output here.

---

**8. Peer employees in the same department (self join)**

```sql
SELECT e1.Name AS Employee, e2.Name AS Peer
FROM Employees e1
JOIN Employees e2 ON e1.DepartmentID = e2.DepartmentID
WHERE e1.EmployeeID <> e2.EmployeeID;
```

**Output:**

| Employee | Peer    |
| -------- | ------- |
| Alice    | Charlie |
| Charlie  | Alice   |
| Bob      | Eve     |
| Eve      | Bob     |

---

**9. Join Employees, Departments, Salaries**

```sql
SELECT e.Name, d.DepartmentName, s.Salary
FROM Employees e
JOIN Departments d ON e.DepartmentID = d.DepartmentID
JOIN Salaries s ON e.EmployeeID = s.EmployeeID;
```

**Output:**

| Name    | DepartmentName | Salary |
| ------- | -------------- | ------ |
| Alice   | HR             | 5000   |
| Bob     | IT             | 6000   |
| Charlie | HR             | 5500   |
| David   | Finance        | 4500   |
| Eve     | IT             | 7000   |

---

**10. Employees without salaries**

```sql
SELECT e.Name
FROM Employees e
LEFT JOIN Salaries s ON e.EmployeeID = s.EmployeeID
WHERE s.Salary IS NULL;
```

**Output:** None, all employees have salaries.

---

**11. Highest-paid employee per department**

```sql
SELECT d.DepartmentName, e.Name, s.Salary
FROM Employees e
JOIN Salaries s ON e.EmployeeID = s.EmployeeID
JOIN Departments d ON e.DepartmentID = d.DepartmentID
WHERE s.Salary = (
    SELECT MAX(s2.Salary)
    FROM Salaries s2
    JOIN Employees e2 ON s2.EmployeeID = e2.EmployeeID
    WHERE e2.DepartmentID = e.DepartmentID
);
```

**Output:**

| DepartmentName | Name    | Salary |
| -------------- | ------- | ------ |
| HR             | Charlie | 5500   |
| IT             | Eve     | 7000   |
| Finance        | David   | 4500   |

---

**12. Employees not assigned to any department**

```sql
SELECT e.Name
FROM Employees e
LEFT JOIN Departments d ON e.DepartmentID = d.DepartmentID
WHERE d.DepartmentID IS NULL;
```

**Output:** None (all employees assigned).

---

**13. Cross join Employees × Departments**

```sql
SELECT e.Name, d.DepartmentName
FROM Employees e
CROSS JOIN Departments d;
```

**Output:** 5 employees × 4 departments = 20 rows (all combinations).

---

**14. Employees reporting to same manager (self join)**

```sql
SELECT e1.Name AS Employee, e2.Name AS Manager
FROM Employees e1
LEFT JOIN Employees e2 ON e1.ManagerID = e2.EmployeeID;
```

**Output:**

| Employee | Manager |
| -------- | ------- |
| Alice    | NULL    |
| Bob      | Alice   |
| Charlie  | Alice   |
| David    | Bob     |
| Eve      | Bob     |

---

**15. Employees earning above department average salary**

```sql
SELECT e.Name, s.Salary, e.DepartmentID
FROM Employees e
JOIN Salaries s ON e.EmployeeID = s.EmployeeID
JOIN (
    SELECT DepartmentID, AVG(s.Salary) AS DeptAvg
    FROM Employees e
    JOIN Salaries s ON e.EmployeeID = s.EmployeeID
    GROUP BY DepartmentID
) dept_avg ON e.DepartmentID = dept_avg.DepartmentID
WHERE s.Salary > dept_avg.DeptAvg;
```

**Output:**

| Name    | Salary | DepartmentID |
| ------- | ------ | ------------ |
| Charlie | 5500   | 10           |
| Eve     | 7000   | 20           |

---

Got it 👍
As a **Senior QC / QA Engineer**, what you’re asking for is a **structured classification of common problems and defects found in database testing**. This is very useful for **test planning, defect reporting, root cause analysis, and audits**.

Below is a **professional, industry-standard categorization** of **database testing bugs**, with examples and what to verify.

---

# Database Testing – Common Problem & Bug Categories

## 1. **Data Integrity & Consistency Issues**

These are the **most critical** database defects.

### Common Bugs

* Orphan records (missing parent data)
* Duplicate records where uniqueness is required
* Incorrect foreign key relationships
* Partial inserts/updates
* Mismatched data across related tables

### Example

* Order exists without a valid Customer
* User deleted but profile still exists

### What to Test

* Primary key / foreign key constraints
* Cascade delete/update behavior
* Referential integrity

---

## 2. **Constraint & Rule Violations**

Bugs related to database rules not being enforced.

### Common Bugs

* NULL values allowed in NOT NULL columns
* Invalid data inserted (out-of-range values)
* Unique constraint not working
* Check constraints ignored

### Example

* Age = -5 stored
* Duplicate email addresses allowed

### What to Test

* NOT NULL
* UNIQUE
* CHECK
* DEFAULT values

---

## 3. **Data Accuracy & Validation Issues**

Data exists, but it’s **wrong**.

### Common Bugs

* Incorrect calculations
* Rounding errors
* Wrong date/time values
* Incorrect status transitions

### Example

* Tax calculation mismatch
* Date stored in wrong timezone

### What to Test

* Business rule validation
* Derived/calculated columns
* Stored procedure logic

---

## 4. **CRUD Operation Issues**

Failures in basic database operations.

### Common Bugs

* Insert succeeds but update fails
* Delete removes wrong records
* Update affects more rows than expected
* Missing rollback on failure

### Example

* Updating one user updates all users

### What to Test

* Insert / Select / Update / Delete
* Transaction commit & rollback
* Row count verification

---

## 5. **Cascade & Referential Action Issues**

Very common in complex systems.

### Common Bugs

* Cascade delete not triggered
* Unexpected cascade delete (data loss)
* Update cascade not working
* Circular cascade failure

### Example

* Parent deleted but children remain
* Deleting user deletes unrelated data

### What to Test

* ON DELETE CASCADE / RESTRICT / SET NULL
* ORM cascade configurations

---

## 6. **Stored Procedures, Functions & Triggers Issues**

Logic-related database bugs.

### Common Bugs

* Procedure not handling edge cases
* Trigger firing multiple times
* Infinite trigger loops
* Incorrect output parameters

### Example

* Audit trigger inserts duplicate logs

### What to Test

* Input/output validation
* Error handling
* Performance impact

---

## 7. **Transaction & Concurrency Issues**

Critical for financial or high-traffic systems.

### Common Bugs

* Dirty reads
* Lost updates
* Deadlocks
* Phantom reads

### Example

* Two users overwrite each other’s data

### What to Test

* Transaction isolation levels
* Locking behavior
* Multi-user scenarios

---

## 8. **Performance & Scalability Issues**

Usually found in production-like data.

### Common Bugs

* Slow queries
* Missing or unused indexes
* Full table scans
* Blocking queries

### Example

* Query works in QA but times out in prod

### What to Test

* Execution plans
* Query response time
* Index usage

---

## 9. **Security & Access Control Issues**

Often overlooked but high risk.

### Common Bugs

* Unauthorized data access
* SQL injection vulnerabilities
* Over-privileged database users
* Sensitive data not encrypted

### Example

* User can see another user’s data

### What to Test

* Role-based access
* Encryption (at rest / in transit)
* Input sanitization

---

## 10. **Data Migration & ETL Issues**

Very common during releases.

### Common Bugs

* Data loss during migration
* Incorrect field mapping
* Truncated data
* Duplicate records post-migration

### Example

* Phone numbers cut off after migration

### What to Test

* Source vs target reconciliation
* Record counts
* Data format validation

---

## 11. **Backup, Recovery & Reliability Issues**

Disaster recovery–related defects.

### Common Bugs

* Backup failure
* Restore does not work
* Inconsistent restored data

### What to Test

* Backup schedules
* Restore verification
* Point-in-time recovery

---

## 12. **Environment & Configuration Issues**

Non-functional but common.

### Common Bugs

* Wrong schema version
* Missing tables or columns
* Incorrect DB parameters

### Example

* QA and PROD schemas don’t match

---

# High-Level Bug Classification (for Defect Tracking)

You can use this **defect type taxonomy** in JIRA / ALM:

* Data Integrity Defect
* Constraint Violation
* Business Rule Defect
* CRUD Defect
* Cascade / Referential Defect
* Stored Procedure / Trigger Defect
* Transaction / Concurrency Defect
* Performance Defect
* Security Defect
* Migration / ETL Defect
* Backup / Recovery Defect
* Configuration Defect

---








