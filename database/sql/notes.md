## Database
- A database is an organized collection of data, typically stored electronically in a computer system. It's designed for efficient storage, retrieval, and management of information. Databases are managed by database management systems (DBMS), which provide tools for interacting with the data.


## SQL(Structured Query Language)
- SQL is a standard programming language for storing, manipulating and retrieving data in databases.


## MYSQL COMMANDS

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
- The SHOW DATABASES is used view all the databases
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

