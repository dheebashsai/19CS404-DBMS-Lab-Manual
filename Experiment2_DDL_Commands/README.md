# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ProductID   Name              Category    Price       Stock
----------  ---------------   ----------  ----------  ----------
106         Fitness Tracker   Wearables
107         Laptop            Electronics  999.99      50
108         Wireless Earbuds  Accessories              100
 

For example:

Test	Result
SELECT * FROM Products;
ProductID   Name             Category    Price       Stock
----------  ---------------  ----------  ----------  ----------
106         Fitness Tracker  Wearables
107         Laptop           Electronic  999.99      50
108         Wireless Earbud  Accessorie              100

```sql
insert into Products(ProductID,Name,Category,Price,Stock) 
values('106','Fitness Tracker','Wearables','',''),
('107','Laptop','Electronic','999.99','50'),
('108','Wireless Earbud','Accessorie','','100');
```

**Output:**

![Output1](<img width="2603" height="541" alt="image" src="https://github.com/user-attachments/assets/db766e0e-fb76-4c89-b3bc-050da587b4ca" />)

**Question 2**
Insert the following customers into the Customers table:

CustomerID  Name         Address     City        ZipCode
----------  -----------  ----------  ----------  ----------
302         Laura Croft  456 Elm St  Seattle     98101
303         Bruce Wayne  789 Oak St  Gotham      10001
For example:

Test	Result
SELECT * FROM Customers;

CustomerID  Name         Address     City        ZipCode
----------  -----------  ----------  ----------  ----------
302         Laura Croft  456 Elm St  Seattle     98101
303         Bruce Wayne  789 Oak St  Gotham      10001
```sql
insert into Customers(CustomerID,Name,Address,City,ZipCode) values(302,'Laura Croft','456 Elm St','Seattle',98101),(303,'Bruce Wayne','789 Oak St','Gotham',10001);
```

**Output:**

![Output2](output.png)

**Question 3**
Create a table named Departments with the following columns:

DepartmentID as INTEGER
DepartmentName as TEXT
For example:

Test	Result
pragma table_info('Departments');
cid    name             type        notnull     dflt_value  pk
-----  ---------------  ----------  ----------  ----------  ----------
0      DepartmentID     INTEGER     0                       0
1      DepartmentName   TEXT        0                       0


```sql
create table Departments(
DepartmentID INTEGER,
DepartmentName TEXT
);
```

**Output:**

![Output3](![WhatsApp Image 2025-09-29 at 14 14 24_03b6b20b](https://github.com/user-attachments/assets/1b9220d1-ee09-4d81-9efd-7dda0ec1745e))

**Question 4**
Write an SQL query to add two new columns, department_id and manager_id, to the table employee with datatype of INTEGER. The manager_id column should have a default value of NULL.
For example:

Test	Result
PRAGMA table_info(employee);
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           salary      number      0                       0
2           department  INTEGER     0                       0
3           manager_id  INTEGER     0           NULL        0


```sql
alter table employee add department_id INTEGER;
alter table employee add manager_id INTEGER default NULL;
```

**Output:**

![Output4](<img width="1795" height="368" alt="image" src="https://github.com/user-attachments/assets/83dc6ac3-5428-4231-9487-8271b27879a5" />)

**Question 5**
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.
For example:

Test	Result
INSERT INTO ProjectAssignments (AssignmentID, EmployeeID, ProjectID, AssignmentDate) VALUES (2, 99, 1, '2024-01-03');
Error: FOREIGN KEY constraint failed


```sql
create table ProjectAssignments(
AssignmentID INTEGER primary key,
EmployeeID integer,
ProjectID integer,
AssignmentDate date not null,
foreign key(EmployeeID) references Employees(EmployeeID),
foreign key(ProjectID) references Projects(ProjectID)
);
```

**Output:**

![Output5](<img width="2310" height="339" alt="image" src="https://github.com/user-attachments/assets/d10625fe-b033-4904-9d50-319388a7b4e1" />)

**Question 6**
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.
For example:

Test	Result
INSERT INTO Invoices (InvoiceID, InvoiceDate)
VALUES (1, '2024-08-08'),(1,'2024-09-08');
Error: UNIQUE constraint failed: Invoices.InvoiceID


```sql
create table Invoices(
InvoiceID integer primary key,
InvoiceDate date,
Duedate date check(DueDate>InvoiceDate),
Amount real check(Amount>0)
);
```

**Output:**

![Output6](<img width="1455" height="171" alt="image" src="https://github.com/user-attachments/assets/7de199f6-465a-4d28-a4c0-8c57851a5aee" />)

**Question 7**
Insert the below data into the Customers table, allowing the City and ZipCode columns to take their default values.

CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St      

Note: The City and ZipCode columns will use their default values.
 
For example:

Test	Result
SELECT CustomerID, Name, Address
FROM Customers;
CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St


```sql
insert into Customers(CustomerID,Name,Address)
values('304','Peter Parker','Spider St');
```

**Output:**

![Output7](<img width="1528" height="333" alt="image" src="https://github.com/user-attachments/assets/69f45619-12de-4e5e-86e6-1f725f39c6ab" />)

**Question 8**
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
INSERT INTO Invoices (InvoiceID, InvoiceDate, Amount, DueDate, OrderID) VALUES (1, '2024-08-01', 100.0, '2024-09-01', 1);
SELECT * FROM Invoices;
InvoiceID   InvoiceDate  Amount      DueDate     OrderID
----------  -----------  ----------  ----------  ----------
1           2024-08-01   100.0       2024-09-01  1

```sql
create table Invoices(
InvoiceID integer primary key,
InvoiceDate date,
Amount real check(amount>0),
DueDate Date check(DueDate>InvoiceDate),
OrderID integer,
foreign key(OrderID) references Orders(OrderID)
);
```

**Output:**

![Output8](<img width="2514" height="366" alt="image" src="https://github.com/user-attachments/assets/7f543d01-dde1-4589-8ca5-ab40f93e17d2" />)

**Question 9**
Write an SQL query to add a new column salary of type INTEGER to the Employees table, with a CHECK constraint that ensures the value in this column is greater than 0.

 

 

For example:

Test	Result
pragma table_info('employees');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           name        TEXT        1                       0
2           salary      INTEGER     0                       0

```sql
alter table Employees add salary INTEGER check(salary>0);
```

**Output:**

![Output9](<img width="2173" height="359" alt="image" src="https://github.com/user-attachments/assets/46b5b2c7-9b9b-4280-bc9b-7c229e603a7a" />)

**Question 10**
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

For example:

Test	Result
select * from Customers;
CustomerID  Name             Address         Email
----------  ---------------  --------------  ---------------------
301         Michael Johnson  123 Elm Street  michael.j@example.com
302         Sarah Lee        456 Oak Avenue  sarah.lee@example.com
303         David Wilson     789 Pine Road   david.w@example.com

```sql
Select CustomerID,Name,Address,Email from Old_customers;
```

**Output:**

![Output10](<img width="1908" height="337" alt="image" src="https://github.com/user-attachments/assets/c00f430b-27b5-4ac7-8ba0-20d7fb96b5bc" />)


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
