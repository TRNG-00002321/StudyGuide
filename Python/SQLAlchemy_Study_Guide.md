# SQLAlchemy

## SQLAlchemy - Introduction
SQLAlchemy is referred to as the toolkit of Python SQL that provides developers with the flexibility of using the SQL database. The benefit of using this particular library is to allow Python developers to work with the language's own objects, and not write separate SQL queries. They can use Python to access and work with databases.  
SQLAlchemy is also an Object Relational Mapper which is a technique used to map data between databases or OOP languages such as Python.  
SQLAlchemy is designed to operate with a DBAPI implementation built for a particular database. It uses dialect system to communicate with various types of DBAPI implementations and databases. All dialects require that an appropriate DBAPI driver is installed.  

The following are the dialects included −
- Firebird
Microsoft SQL Server 
- MySQL
- Oracle
- PostgreSQL
- SQLite
- Sybase  

**SQLAlchemy - Installation**  
`pip install sqlalchemy`

## SQLAlchemy Core Expression Language  

`SQLAlchemy core` includes `SQL rendering engine, DBAPI integration, transaction integration, and schema description services`. SQLAlchemy core uses `SQL Expression Language` that provides a schema-centric usage paradigm whereas `SQLAlchemy ORM` is a domain-centric mode of usage.  

The `SQL Expression Language` presents a system of representing relational database structures and expressions using Python constructs. It presents a system of representing the primitive constructs of the relational database.  

Expression Language is one of the core components of SQLAlchemy. It allows the programmer to specify SQL statements in Python code and use it directly in more complex queries. Expression language is independent of backend and comprehensively covers every aspect of raw SQL. It is closer to raw SQL than any other component in SQLAlchemy.  

Statements of Expression language will be translated into corresponding raw SQL queries by SQLAlchemy engine.  

## Connecting to the Database
`Engine` class connects a `Pool` and `Dialect` together to provide a source of database connectivity and behavior. An object of Engine class is instantiated using the `create_engine()` function.  
The create_engine() function takes the database as one argument. The database is not needed to be defined anywhere. The standard calling form has to send the URL as the first positional argument, usually a string that indicates database dialect and connection arguments.  
To connect to a database in order to access the data and work with it, we need to first establish a connection by using the following command:
```python
    from sqlalchemy import create_engine
    engine = create_engine("sqlite:///mydatabase.db") # Example for SQLite
```   
The `create_engine()` function returns an `Engine` object. Some important methods of Engine class are −  	
- ***connect()*** : Returns connection object
- ***execute()*** : Executes a SQL statement construct
- ***begin()*** : Returns a context manager delivering a Connection with a Transaction established. Upon successful operation, the Transaction is committed, else it is rolled back
- ***dispose()*** : Disposes of the connection pool used by the Engine
- ***driver()***: Driver name of the Dialect in use by the Engine
- ***table_names()*** : Returns a list of all table names available in the database
- ***transaction()*** : Executes the given function within a transaction boundary  

## SQLAlchemy Core - Creating Table
Creating tables in SQLAlchemy can be done using either SQLAlchemy Core or SQLAlchemy ORM.  
- ***MetaData object***: This object will act as a container for your table definitions.  
- ***De*fine your table***: Use the Table constructor, providing the table name, the MetaData object, and Column objects for each column.
- ***Create the table(s) in the database***: Use `meta.create_all(engine)`. This will create all tables associated with the MetaData object in the specified engine.
```python
from sqlalchemy import create_engine, MetaData, Table, Column, Integer, String
engine = create_engine('sqlite:///C:/2025Training/TRNG-00002321/sqlite_demo/college.db', echo = True)
meta = MetaData()

students = Table(
   'students', meta,
   Column('id', Integer, primary_key = True),
   Column('name', String),
   Column('lastname', String),
)
meta.create_all(engine)
```  

## SQLAlchemy Core - SQL Expressions
SQLAlchemy's SQL Expression Language provides a Pythonic way to construct and represent SQL statements. It allows users to build queries, define tables and columns, and interact with the database using Python objects rather than raw SQL strings. This offers benefits such as type safety, database independence (to a degree), and easier manipulation of complex queries.  

### Key elements of the SQLAlchemy SQL Expression Language

**Table and Column Objects:**  
***Table***: Represents a database table.  
***Column***: Represents a column within a table, including its name, data type, and constraints.  
```python
    from sqlalchemy import Table, Column, Integer, String, MetaData

    metadata = MetaData()
    users_table = Table('users', metadata,
                        Column('id', Integer, primary_key=True),
                        Column('name', String),
                        Column('email', String))
```  

**SQL Expressions**
- ***Column Elements***: Basic building blocks like Column objects, which can be used in expressions.
- ***Operators***: Python operators `(==, !=, <, >)` and SQLAlchemy-specific functions (e.g., and_, or_, like) are overloaded to construct SQL expressions.
- ***Functions***: SQL functions like `count(), sum(), avg()` can be used.  
```python
    from sqlalchemy import select, and_

    # Example using operators
    stmt = select(users_table).where(users_table.c.name == 'Alice')

    # Example using and_() for multiple conditions
    stmt_complex = select(users_table).where(
        and_(users_table.c.name == 'Bob', users_table.c.email.like('%example.com%'))
    )
```
**Statements**
- ***select()***: Constructs SELECT statements.
- ***insert()***: Constructs INSERT statements.
- ***update()***: Constructs UPDATE statements.
- ***delete()***: Constructs DELETE statements.  
```python
    from sqlalchemy import insert, update, delete

    # Insert statement
    insert_stmt = insert(users_table).values(name='Charlie', email='charlie@example.com')

    # Update statement
    update_stmt = update(users_table).where(users_table.c.name == 'Alice').values(email='alice_new@example.com')

    # Delete statement
    delete_stmt = delete(users_table).where(users_table.c.name == 'Bob')
```

**Executing Expression**
Executing an expression in SQLAlchemy, whether it's a SQL Expression Language construct or a raw SQL string, typically involves using the `execute()` method of a connection object.

```python
from sqlalchemy import Table, Column, Integer, String, MetaData, select

# Define a table (example)
metadata = MetaData()
users = Table('users', metadata,
              Column('id', Integer, primary_key=True),
              Column('name', String))

# Create a select statement
s = select(users).where(users.c.name == "Alice")

# Execute the statement
result = connection.execute(s)

# Fetch results (e.g., all rows)
rows = result.fetchall()
print(rows)
```
**Selecting Rows**
Selecting rows in SQLAlchemy Core involves constructing a Select object and then executing it against a database connection. This process allows for retrieving data from tables, potentially with filtering and column selection.  

***Basic Row Selection (All Columns)***
```python
from sqlalchemy import create_engine, MetaData, Table, Column, Integer, String, select
engine = create_engine('sqlite:///C:/2025Training/TRNG-00002321/sqlite_demo/college.db', echo = True)
meta = MetaData()

students = Table(
   'students', meta,
   Column('id', Integer, primary_key = True),
   Column('name', String),
   Column('email', String),
)
meta.create_all(engine)
# Construct the SELECT statement
stmt = select(students)

# Execute the statement and fetch results
with engine.connect() as connection:
    result = connection.execute(stmt)
    for row in result:
        print(row)
```

***Selecting Specific Columns:***
To retrieve only specific columns, pass those Column objects to the select() function:  
```python
stmt = select(students.c.name, students.c.email)
```

***Filtering Rows with WHERE Clause***
Use the .where() method on the Select object to add filtering conditions:
```python
stmt=select(students).where(students.c.name == 'Charlie')
```

**Fetching Results:**
- ***connection.execute(stmt)*** returns a Result object.
- Iterate directly over the ***Result object*** to get individual rows.
- ***result.fetchone()*** fetches the next row.
- ***result.fetchall()*** fetches all remaining rows as a list.
- ***result.scalar()*** fetches a single scalar value if the query returns one column and one row.
- ***result.scalars()*** fetches a single scalar value per row if the query returns one column.  

## Using Textual SQL
SQLAlchemy lets you just use strings, for those cases when the SQL is already known and there isnt a strong need for the statement to support dynamic features. The `text()` construct is used to compose a textual statement that is passed to the database mostly unchanged.

It constructs a new `TextClause`, representing a textual SQL string directly
```python
from sqlalchemy import text
t = text("SELECT * FROM students")
result = connection.execute(t)
```

The `text()` function requires `Bound parameters` in the named colon format. They are consistent regardless of database backend. To send values in for the parameters, we pass them into the `execute()` method as additional arguments.
```python
from sqlalchemy.sql import text
s = text("select students.name, students.lastname from students where students.name between :x and :y")
conn.execute(s, x = 'A', y = 'L').fetchall()
```  
The text() construct supports pre-established bound values using the `TextClause.bindparams()` method.
```python
stmt = text("SELECT * FROM students WHERE students.name BETWEEN :x AND :y")

stmt = stmt.bindparams(
   bindparam("x", type_= String), 
   bindparam("y", type_= String)
)

result = conn.execute(stmt, {"x": "A", "y": "L"})
```

You can also use `and_()` function to combine multiple conditions in WHERE clause created with the help of text() function
```python
from sqlalchemy import and_
from sqlalchemy.sql import select
s = select([text("* from students")]) \
.where(
   and_(
      text("students.name between :x and :y"),
      text("students.id>2")
   )
)
conn.execute(s, x = 'A', y = 'L').fetchall()
```

## SQLAlchemy Core - Using Aliases
The SQLAlchemy `alias()` method is used to create a temporary, alternative name for a table or a selectable object (like a select() construct or a subquery) within a SQL query. This is analogous to using the `AS` keyword in standard SQL.

``` python
from sqlalchemy import Table, Column, Integer, String, MetaData, select
    
    metadata = MetaData()
    users = Table('users', metadata,
                  Column('id', Integer, primary_key=True),
                  Column('name', String))
    
    # Create an alias for the 'users' table
    u_alias = users.alias("u")
    
    # Use the alias in a select statement
    s = select(u_alias.c.name).where(u_alias.c.id > 5)
```

## Using UPDATE Expression
The `update()` method on target table object constructs equivalent UPDATE SQL expression.  
`table.update().where(conditions).values(SET expressions)`

```python
stmt = students.update().where(students.c.lastname == 'Khanna').values(lastname = 'Kapoor')
```

## Using DELETE Expression
The delete operation can be achieved by running `delete()` method on target table object as given in the following statement −
`stmt = students.delete()`
```python
stmt = students.delete().where(students.c.id > 2)
```

