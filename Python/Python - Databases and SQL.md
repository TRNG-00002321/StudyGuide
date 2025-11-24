# Python - Databases and SQL
The Python programming language has powerful features for database programming. Python supports various databases like SQLite, MySQL, Oracle, Sybase, PostgreSQL, etc. Python also supports Data Definition Language (DDL), Data Manipulation Language (DML) and Data Query Statements. The Python standard for database interfaces is the Python DB-API. Most Python database interfaces adhere to this standard.  

## Connect To Database
To connect to an existing database use the `connect()` method. If the database does not exist, then it will be created and finally a database object will be returned.

```python
import sqlite3
conn = sqlite3.connect('C:\\2025Training\\TRNG-00002321\\sqlite_demo\\test.db')
print ("Opened database successfully")
```
> You can also supply database name as the special name `:memory:` to create a database in RAM.  
## Creating a Cursor Object
Obtain a cursor object from the established connection. The cursor acts as an intermediary, allowing you to execute SQL commands and fetch results.

## Executing SQL Queries
Use the cursor's `execute()` method to run SQL statements for tasks like  
- Creating databases and tables (CREATE DATABASE, CREATE TABLE).
- Inserting data (INSERT INTO).
- Retrieving data (SELECT).
- Updating data (UPDATE).
- Deleting data (DELETE FROM).

## Fetching Results
For `SELECT` queries, using methods like `fetchone()`, `fetchmany()`, or `fetchall()` on the cursor to retrieve the query results. These methods return data as tuples or lists of tuples.  

## Committing and Closing:
- Committing changes to the database using `connection.commit()` for operations that modify data (e.g., INSERT, UPDATE, DELETE).
- Closing the cursor and the database connection using `cursor.close()` and connection.close() to release resources.

```python
import sqlite3

# Connect to a database (or create it if it doesn't exist)
conn = sqlite3.connect('C:\\2025Training\\TRNG-00002321\\sqlite_demo\\example.db')
cursor = conn.cursor()

# Create a table
cursor.execute('''
    CREATE TABLE IF NOT EXISTS users (
        id INTEGER PRIMARY KEY,
        name TEXT,
        email TEXT
    )
''')

# Insert data
cursor.execute("INSERT INTO users (name, email) VALUES (?, ?)", ('Alice', 'alice@example.com'))
cursor.execute("INSERT INTO users (name, email) VALUES (?, ?)", ('Bob', 'bob@example.com'))

# Commit the changes
conn.commit()

# Query data
cursor.execute("SELECT * FROM users")
rows = cursor.fetchall()

print("Users in the database:")
for row in rows:
    print(row)

# Close the connection
conn.close()
```

## Parameterized Queries: 
Use placeholders (like ? for SQLite or %s for MySQL/PostgreSQL) to prevent SQL injection vulnerabilities.

```python
import sqlite3

conn = sqlite3.connect('C:\\2025Training\\TRNG-00002321\\sqlite_demo\\example.db')
cursor = conn.cursor()

# Create a table (if it doesn't exist)
cursor.execute('''
    CREATE TABLE IF NOT EXISTS users01 (
        id INTEGER PRIMARY KEY,
        name TEXT,
        age INTEGER
    )
''')

# Insert data using parameterized query
user_name = "Alice"
user_age = 30
cursor.execute("INSERT INTO users01 (name, age) VALUES (?, ?)", (user_name, user_age))

# Select data using parameterized query
min_age = 25
cursor.execute("SELECT name, age FROM users01 WHERE age > ?", (min_age,))
results = cursor.fetchall()
for row in results:
    print(f"Name: {row[0]}, Age: {row[1]}")

conn.commit()
conn.close()
```
