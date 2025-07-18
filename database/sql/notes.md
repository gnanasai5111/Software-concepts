## Database
- A database is an organized collection of data, typically stored electronically in a computer system. It's designed for efficient storage, retrieval, and management of information. Databases are managed by database management systems (DBMS), which provide tools for interacting with the data.


## SQL(Structured Query Language)
- SQL is a standard programming language for storing, manipulating and retrieving data in databases.

### CREATE DATABASE
- The CREATE DATABASE is used to create a new database.
```
CREATE DATABASE databasename;
```

### DROP DATABASE
- The DROP DATABASE is used to drop an existing database.
```
DROP DATABASE databasename;
```

### SHOW DATABASES
- The SHOW DATABASES is used to List all available databases.
```
SHOW DATABASES;
```
### BACKUP DATABASE
- The BACKUP DATABASE is used for creating backup of the database
```
BACKUP DATABASE databasename to DISK='filepath'
```
- A differential back up only backs up the parts of the database that have changed since the last full database backup.
```
BACKUP DATABASE databasename to DISK='filepath' WITH DIFFERENTIAL
```

### CREATE TABLE
- The CREATE TABLE statement is used to create a new table in a database.
```
CREATE TABLE tablename (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
);
```
**Example**
```
CREATE TABLE Employees (
    EmployeeID,
    Name VARCHAR(100),
    Email VARCHAR(150),
    Gender ENUM('Male', 'Female', 'Other'),
    IsActive BOOLEAN,
    Salary DECIMAL(10, 2),
    JoinDate DATE,
    LastLogin DATETIME,
    ProfileImage BLOB,
    Metadata JSON
);
```

### DROP TABLE 
-  It is used to delete the table from the database
```
DROP TABLE tablename;
```

### TRUNCATE TABLE
- It is used to delete the data inside a table, but not the table itself.
```
TRUNCATE TABLE tablename;
```

### ALTER TABLE
- It is is used to add, delete, or modify columns in an existing table.

**Add Column**
```
ALTER TABLE tablename
ADD columnname datatype;
```
**Remove Column**
```
ALTER TABLE tablename
DROP COLUMN columnname;
```
**Rename Column**
```
ALTER TABLE tablename
RENAME COLUMN old_name to new_name;
```
**Change Datatype**
```
ALTER TABLE table_name
MODIFY COLUMN column_name datatype;
```

Here are concise and complete **SQL Constraints Notes**, including all key types of constraints with syntax and examples:

---

## SQL Constraints

Constraints are rules applied to table columns to enforce data integrity and accuracy.

### 1. NOT NULL
- Ensures that a column cannot have NULL values.

```
CREATE TABLE Users (
    id INT NOT NULL,
    name VARCHAR(100) NOT NULL
);
```

### 2. UNIQUE

- Ensures that all values in a column are different.
- Can be applied to multiple columns (composite unique).

```
CREATE TABLE Employees (
    emp_id INT,
    email VARCHAR(100) UNIQUE
);
```

```
CONSTRAINT unique_emp UNIQUE(emp_id, email)
```

### 3. PRIMARY KEY

- Uniquely identifies each record.
- Only one primary key per table.
- Automatically implies `NOT NULL` and `UNIQUE`.

```
CREATE TABLE Students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

```
-- Composite primary key
CREATE TABLE Orders (
    order_id INT,
    product_id INT,
    CONSTRAINT pk_order PRIMARY KEY(order_id, product_id)
);
```

### 4. FOREIGN KEY

- Establishes a relationship between two tables.
- References the primary key of another table.

```
CREATE TABLE Departments (
    dept_id INT PRIMARY KEY,
    name VARCHAR(100)
);

CREATE TABLE Employees (
    emp_id INT PRIMARY KEY,
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES Departments(dept_id)
);
```

- You can have multiple foreign keys, even to the same table.

### 5. CHECK

- Limits the range of values for a column.

```
CREATE TABLE Products (
    price DECIMAL(10,2),
    CHECK (price >= 0)
);
```

### 6. DEFAULT

- Provides a default value if no value is provided.

```
CREATE TABLE Users (
    status VARCHAR(20) DEFAULT 'active'
);
```

### 7. AUTO INCREMENT

- Automatically increments numeric values.
- Often used with primary keys.

```
CREATE TABLE Customers (
    customer_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100)
);
```

### 8. INDEX (for performance, not integrity)

- Speeds up SELECT queries.
- Doesn’t enforce uniqueness by default.

```
CREATE INDEX idx_email ON Users(email);
```


### 9. NAMED CONSTRAINTS

- Useful for referencing later or dropping.

```
CONSTRAINT fk_dept FOREIGN KEY (dept_id) REFERENCES Departments(dept_id)
```




