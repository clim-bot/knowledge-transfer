# PostgreSQL Command Line Interface (psql) Cheat Sheet

## Connecting to PostgreSQL
- Open psql with a specific user:
```sh
psql -U username
```

- Connect to a specific database:
```sh
psql -U username -d database_name
```

- Connect to a specific database on a specific host:
```sh
psql -h host -U username -d database_name
```

- Exit psql:
```sh
\q
```

## Database Operations
- Create a new database:
```sh
CREATE DATABASE database_name;
```

- Drop (delete) a database:
```sh
DROP DATABASE database_name;
```

- List all databases:
```sh
\l
```

## User Operations
- Create a new user:
```sh
CREATE USER username WITH PASSWORD 'password';
```

- Drop (delete) a user:
```sh
DROP USER username;
```

- Grant all privileges on a database to a user:
```sh
GRANT ALL PRIVILEGES ON DATABASE database_name TO username;
```

## Table Operations
- Create a new table:
```sh
CREATE TABLE table_name (
  column1 datatype PRIMARY KEY,
  column2 datatype,
  column3 datatype
);
```

- Drop (delete) a table:
```sh
DROP TABLE table_name;
```

- Insert data into a table:
```sh
INSERT INTO table_name (column1, column2, column3) VALUES (value1, value2, value3);
```

- Select data from a table:
```sh
SELECT * FROM table_name;
```

- Update data in a table:
```sh
UPDATE table_name SET column1 = value1 WHERE condition;
```

- Delete data from a table:
```sh
DELETE FROM table_name WHERE condition;
```

## Schema Operations
- List all tables in the current database:
```sh
\dt
```

- Describe a table (show columns and data types):
```sh
\d table_name
```

- List all users:
```sh
\du
```

## Miscellaneous Commands
- Execute a SQL script file:
```sh
\i /path/to/script.sql
```

- Get help on SQL commands:
```sh
\h
```

- Get help on a specific SQL command:
```sh
\h command_name
```

- Show current connection info:
```sh
\conninfo
```

## Notes
- Replace username, database_name, table_name, column1, datatype, value1, and condition with your specific names and values.
- To run these commands, you need appropriate privileges.


Feel free to let me know if you need any more information or additional commands!