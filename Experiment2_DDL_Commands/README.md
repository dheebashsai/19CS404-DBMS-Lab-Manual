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
--
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
303         Bruce Wayne  789 Oak St  Gotham      10001

```sql
insert into Customers(CustomerID,Name,Address,City,ZipCode) values(302,'Laura Croft','456 Elm St','Seattle',98101),(303,'Bruce Wayne','789 Oak St','Gotham',10001);
```

**Output:**

<img width="1219" height="266" alt="image" src="https://github.com/user-attachments/assets/89f28756-ad63-40a4-bd47-71ffd8e04524" />


**Question 2**
---
Write a SQL Query  to add attribute ISBN as varchar(30) and domain_dept as varchar(30) in the table 'books'

For example:

Test	Result
pragma table_info('books');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           book_id     INT         0                       1
1           title       VARCHAR(15  0                       0
2           author      VARCHAR(10  0                       0
3           genre       VARCHAR(50  0                       0
4           publicatio  INT         0                       0
5           ISBN        varchar(30  0                       0
6           domain_dep  varchar(30  0                       0


```sql
alter table books add ISBN varchar(30);
alter table books add domain_dep varchar(30);
```

**Output:**

<img width="1250" height="253" alt="image" src="https://github.com/user-attachments/assets/43ba0905-c06d-4f11-af58-008095ae8b24" />


**Question 3**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700         COM5


```sql
create table item(
    item_id text primary key,
    item_desc text not null,
    rate integer not null,
    icom_id text(4),
    foreign key(icom_id) references company(com_id) on update cascade on delete cascade
    );
```

**Output:**

<img width="1213" height="232" alt="image" src="https://github.com/user-attachments/assets/dc0657c9-c2d1-4a73-88b2-40bfb28c68b5" />


**Question 4**
---
Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.
For example:

Test	Result
INSERT INTO Department (DepartmentID, DepartmentName, Location) VALUES (1, 'Human Resources', 'New York');
select * from Department;
DepartmentID  DepartmentName   Location
------------  ---------------  ----------
1             Human Resources  New York


```sql
create table Department(
    DepartmentID integer primary key,
    DepartmentName text unique not null,
    Location text
    );
```

**Output:**

<img width="1890" height="189" alt="image" src="https://github.com/user-attachments/assets/3d01412b-02f0-40eb-bcd4-a4773f859deb" />


**Question 5**
---
Write a SQL Query  to Rename attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date,State as varchar(30) in the table Companies. 

For example:

Test	Result
pragma table_info('Companies');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          int         0                       0
1           first_name  varchar(50  0                       0
2           address     text        0                       0
3           email       varchar(50  0                       0
4           phone       varchar(10  0                       0
5           mobilenumb  number      0                       0
6           DOB         Date        0                       0
7           State       varchar(30  0                       0


```sql
alter table Companies rename column name to first_name;
alter table Companies add mobilenumber number;
alter table Companies add DOB Date;
alter table Companies add State varchar(30);
```

**Output:**

<img width="1357" height="286" alt="image" src="https://github.com/user-attachments/assets/7afdf64f-aab2-49fe-ab36-0a2356bb12ee" />

**Question 6**
---
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

<img width="1379" height="248" alt="image" src="https://github.com/user-attachments/assets/9c80caa3-ab22-451b-b38a-fb3efa820ca5" />


**Question 7**
---
Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.
For example:

Test	Result
INSERT INTO Products
VALUES (1, NULL,0,5);
Error: NOT NULL constraint failed: Products.ProductName


```sql
create table Products(
    ProductID primary key,
    ProductName not null,
    Price real check(Price>0),
    Stock integer check(Stock>=0)
    );
```

**Output:**

<img width="1091" height="187" alt="image" src="https://github.com/user-attachments/assets/21965331-60a1-4baf-9a95-dc15525eb2f5" />


**Question 8**
---
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
    AssignmentID integer primary key,
    EmployeeID integer,
    ProjectID integer,
    AssignmentDate date not null,
    foreign key(EmployeeID) references Employees(EmployeeID),
    foreign key(ProjectID) references Projects(ProjectID)
    );
```

**Output:**

<img width="1791" height="200" alt="image" src="https://github.com/user-attachments/assets/e386bc58-8b2f-42d3-98b5-4883881584ad" />


**Question 9**
---
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary

For example:

Test	Result
select * from Employee;
EmployeeID  Name        Department  Salary
----------  ----------  ----------  ----------
201         John Doe    HR          50000
202         Jane Smith  Engineerin  75000
203         Emily Davi  Marketing   60000


```sql
select EmployeeID,Name,Department,Salary From Former_employees;
```

**Output:**

<img width="1002" height="203" alt="image" src="https://github.com/user-attachments/assets/ba051b5b-e9e1-43b7-9bf9-d5ff43e799f9" />


**Question 10**
---
Insert the below data into the Student_details table, allowing the Subject and MARKS columns to take their default values.

RollNo      Name          Gender      
----------  ------------  ----------  
204         Samuel Black  M          

Note: The Subject and MARKS columns will use their default values.
 
For example:

Test	Result
SELECT RollNo, Name, Gender 
FROM Student_details 
WHERE RollNo = 204;


RollNo      Name          Gender
----------  ------------  ----------
204         Samuel Black  M

```sql
insert into Student_details(RollNo,Name,Gender) values(204,'Samuel Black','M');
```

**Output:**

<img width="979" height="241" alt="image" src="https://github.com/user-attachments/assets/451c8fe7-36c9-4332-9c0a-f64917114d66" />

## Screenshot of Module 1 SEB Completion Grades

<img width="1135" height="311" alt="image" src="https://github.com/user-attachments/assets/023d75e3-03aa-48a0-8157-f1ae41947803" />

## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
