# SQLAlchemy ORM

The main objective of the Object Relational Mapper API of SQLAlchemy is to facilitate associating user-defined Python classes with database tables, and objects of those classes with rows in their corresponding tables. Changes in states of objects and rows are synchronously matched with each other. SQLAlchemy enables expressing database queries in terms of user defined classes and their defined relationships.

The ORM is constructed on top of the SQL Expression Language. It is a high level and abstracted pattern of usage. In fact, ORM is an applied usage of the Expression Language.

## SQLAlchemy ORM - Declare Mapping
First of all, `create_engine()` function is called to set up an engine object which is subsequently used to perform SQL operations. The function has two arguments, one is the name of database and other is an echo parameter when set to True will generate the activity log. If it doesnot exist, the database will be created.  
```python
from sqlalchemy import create_engine
engine = create_engine('sqlite:///sales.db', echo = True)
```

The Engine establishes a real DBAPI connection to the database when a method like Engine.execute() or Engine.connect() is called. It is then used to emit the SQLORM which does not use the Engine directly; instead, it is used behind the scenes by the ORM.  
In case of ORM, the configurational process starts by describing the database tables and then by defining classes which will be mapped to those tables. In SQLAlchemy, these two tasks are performed together. This is done by using Declarative system; the classes created include directives to describe the actual database table they are mapped to.  
A base class stores a catlog of classes and mapped tables in the Declarative system. This is called as the declarative base class. There will be usually just one instance of this base in a commonly imported module. The declarative_base() function is used to create base class. This function is defined in sqlalchemy.ext.declarative module.  
```python
from sqlalchemy.ext.declarative import declarative_base
Base = declarative_base()
```  
Once base classis declared, any number of mapped classes can be defined in terms of it. Following code defines a Customers class. It contains the table to be mapped to, and names and datatypes of columns in it.  
```python
class Customers(Base):
   __tablename__ = 'customers'
   
   id = Column(Integer, primary_key = True)
   name = Column(String)
   address = Column(String)
   email = Column(String)
```
A class in Declarative must have a `__tablename__` attribute, and at least one Column which is part of a primary key. Declarative replaces all the Column objects with special Python accessors known as descriptors. This process is known as instrumentation which provides the means to refer to the table in a SQL context and enables persisting and loading the values of columns from the database.  
This mapped class like a normal Python class has attributes and methods as per the requirement.  
The information about class in Declarative system, is called as table metadata. SQLAlchemy uses Table object to represent this information for a specific table created by Declarative. The Table object is created according to the specifications, and is associated with the class by constructing a Mapper object. This mapper object is not directly used but is used internally as interface between mapped class and table.  
Each Table object is a member of larger collection known as MetaData and this object is available using the .metadata attribute of declarative base class. The MetaData.create_all() method is, passing in our Engine as a source of database connectivity. For all tables that havent been created yet, it issues CREATE TABLE statements to the database.  
```python
from sqlalchemy import Column, Integer, String
from sqlalchemy import create_engine
engine = create_engine('sqlite:///sales.db', echo = True)
#from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import declarative_base
Base = declarative_base()

class Customers(Base):
   __tablename__ = 'customers'
   id = Column(Integer, primary_key=True)

   name = Column(String)
   address = Column(String)
   email = Column(String)
Base.metadata.create_all(engine)
```

## Creating Session
In order to interact with the database, we need to obtain its handle. A `session` object is the handle to database. Session class is defined using `sessionmaker()` a configurable session factory method which is bound to the engine object created earlier.
```python
from sqlalchemy.orm import sessionmaker
Session = sessionmaker(bind = engine)
```
The session object is then set up using its default constructor as follows −  
`session = Session()`  
Some of the frequently required methods of session class are listed below   
- ***begin()*** : begins a transaction on this session
- ***add()*** : places an object in the session. Its state is persisted in the database on next flush operation
- ***add_all()*** : adds a collection of objects to the session
- ***commit()*** : flushes all items and any transaction in progress
- ***delete()*** : marks a transaction as deleted
- ***execute()*** : executes a SQL expression
- ***expire()*** : marks attributes of an instance as out of date
- ***flush()*** : flushes all object changes to the database
- ***invalidate()*** : closes the session using connection invalidation
- ***rollback()*** : rolls back the current transaction in progress
- ***close()*** : Closes current session by clearing all items and ending any transaction in progress  

## Adding Objects
Declare an object of the class and persistently add it to the table by `add()` method of session object
```python
c1 = Sales(name = 'Ravi Kumar', address = 'Station Road Nanded', email = 'ravi@gmail.com')
session.add(c1)
```
Note that this transaction is pending until the same is flushed using `commit()` method.
```python
session.commit()
```  

```python
from sqlalchemy import Column, Integer, String
from sqlalchemy import create_engine
engine = create_engine('sqlite:///sales.db', echo = True)
from sqlalchemy.ext.declarative import declarative_base
Base = declarative_base()

class Customers(Base):
   __tablename__ = 'customers'
   
   id = Column(Integer, primary_key=True)
   name = Column(String)
   address = Column(String)
   email = Column(String)
   
from sqlalchemy.orm import sessionmaker
Session = sessionmaker(bind = engine)
session = Session()

c1 = Customers(name = 'Ravi Kumar', address = 'Station Road Nanded', email = 'ravi@gmail.com')

session.add(c1)
session.commit()
```

To add multiple records, we can use `add_all()` method of the session class.
```python
session.add_all([
   Customers(name = 'Komal Pande', address = 'Koti, Hyderabad', email = 'komal@gmail.com'), 
   Customers(name = 'Rajender Nath', address = 'Sector 40, Gurgaon', email = 'nath@gmail.com'), 
   Customers(name = 'S.M.Krishna', address = 'Budhwar Peth, Pune', email = 'smk@gmail.com')]
)

session.commit()
```
## Using Query
All SELECT statements generated by SQLAlchemy ORM are constructed by `Query` object. It provides a generative interface, hence successive calls return a new Query object, a copy of the former with additional criteria and options associated with it.  
Query objects are initially generated using the `query()` method of the Session as follows −  
```python
q = session.query(mapped class)
OR
q = Query(mappedClass, session)
```
The query object has all() method which returns a resultset in the form of list of objects. If we execute it on our customers table −
```python
result = session.query(Customers).all()
```  
The result object can be traversed using For loop as below to obtain all records in underlying customers table.  
```python
from sqlalchemy import Column, Integer, String
from sqlalchemy import create_engine
engine = create_engine('sqlite:///sales.db', echo = True)
from sqlalchemy.ext.declarative import declarative_base
Base = declarative_base()

class Customers(Base):
   __tablename__ = 'customers'
   id = Column(Integer, primary_key =  True)
   name = Column(String)

   address = Column(String)
   email = Column(String)

from sqlalchemy.orm import sessionmaker
Session = sessionmaker(bind = engine)
session = Session()
result = session.query(Customers).all()

for row in result:
   print ("Name: ",row.name, "Address:",row.address, "Email:",row.email)
```

The Query object also has following useful methods −   
- ***add_columns()*** : It adds one or more column expressions to the list of result columns to be returned.
- ***add_entity()*** : It adds a mapped entity to the list of result columns to be returned.
- ***count()*** : It returns a count of rows this Query would return.
- ***delete()*** : It performs a bulk delete query. Deletes rows matched by this query from the database.
- ***distinct()*** : It applies a DISTINCT clause to the query and return the newly resulting Query.
- ***filter()*** : It applies the given filtering criterion to a copy of this Query, using SQL expressions.
- ***first()*** : It returns the first result of this Query or None if the result doesnt contain any row.
- ***get()*** : It returns an instance based on the given primary key identifier providing direct access to the identity map of the owning Session.
- ***group_by()*** : It applies one or more GROUP BY criterion to the query and return the newly resulting Query
- ***join()*** : It creates a SQL JOIN against this Query objects criterion and apply generatively, returning the newly resulting Query.
- ***one()*** : It returns exactly one result or raise an exception.
- ***order_by()*** : It applies one or more ORDER BY criterion to the query and returns the newly resulting Query.
- ***update()*** : It performs a bulk update query and updates rows matched by this query in the database.  

## Updating Objects
To modify data of a certain attribute of any object, we have to assign new value to it and commit the changes to make the change persistent.
```python
x = session.query(Customers).get(2)
x.address = 'Banjara Hills Secunderabad'
session.commit()
```  
For bulk updates, use `update()` method of the Query object. 
```python
session.query(Customers).filter(Customers.id! = 2).
update({Customers.name:"Mr."+Customers.name}, synchronize_session = False)
```  
The update() method requires two parameters as follows −

- A dictionary of key-values with key being the attribute to be updated, and value being the new contents of attribute.
- synchronize_session attribute mentioning the strategy to update attributes in the session. Valid values are false: for not synchronizing the session, fetch: performs a select query before the update to find objects that are matched by the update query; and evaluate: evaluate criteria on objects in the session.

## Applying Filter
Resultset represented by Query object can be subjected to certain criteria by using `filter()` method. The general usage of filter method is as follows −  
`session.query(class).filter(criteria)`  

In the following example, resultset obtained by SELECT query on Customers table is filtered by a condition, (ID>2) −
```python
result = session.query(Customers).filter(Customers.id>2)
```  
```python
from sqlalchemy import Column, Integer, String
from sqlalchemy import create_engine
engine = create_engine('sqlite:///sales.db', echo = True)
from sqlalchemy.ext.declarative import declarative_base
Base = declarative_base()

class Customers(Base):
   __tablename__ = 'customers'
   
   id = Column(Integer, primary_key = True)
   name = Column(String)

   address = Column(String)
   email = Column(String)

from sqlalchemy.orm import sessionmaker
Session = sessionmaker(bind = engine)
session = Session()
result = session.query(Customers).filter(Customers.id>2)

for row in result:
   print ("ID:", row.id, "Name: ",row.name, "Address:",row.address, "Email:",row.email)
```

## Filter Operators
**Equals**  
The usual operator used is == and it applies the criteria to check equality.  
```python
result = session.query(Customers).filter(Customers.id == 2)

for row in result:
   print ("ID:", row.id, "Name: ",row.name, "Address:",row.address, "Email:",row.email)
```

**Not Equals**  
The operator used for not equals is != and it provides not equals criteria.  
```python
result = session.query(Customers).filter(Customers.id! = 2)

for row in result:
   print ("ID:", row.id, "Name: ",row.name, "Address:",row.address, "Email:",row.email)
```
**Like**  
like() method itself produces the LIKE criteria for WHERE clause in the SELECT expression.  
```python
result = session.query(Customers).filter(Customers.name.like('Ra%'))
for row in result:
   print ("ID:", row.id, "Name: ",row.name, "Address:",row.address, "Email:",row.email)
```
**IN**  
This operator checks whether the column value belongs to a collection of items in a list. It is provided by in_() method.
```python
result = session.query(Customers).filter(Customers.id.in_([1,3]))
for row in result:
   print ("ID:", row.id, "Name: ",row.name, "Address:",row.address, "Email:",row.email)
```
**AND**  
This conjunction is generated by either putting multiple commas separated criteria in the filter or using and_() method as given below −
```python
result = session.query(Customers).filter(Customers.id>2, Customers.name.like('Ra%'))
for row in result:
   print ("ID:", row.id, "Name: ",row.name, "Address:",row.address, "Email:",row.email)
```  
```python
from sqlalchemy import and_
result = session.query(Customers).filter(and_(Customers.id>2, Customers.name.like('Ra%')))

for row in result:
   print ("ID:", row.id, "Name: ",row.name, "Address:",row.address, "Email:",row.email)
```  
**OR**  
This conjunction is implemented by or_() method.
```python
from sqlalchemy import or_
result = session.query(Customers).filter(or_(Customers.id>2, Customers.name.like('Ra%')))

for row in result:
   print ("ID:", row.id, "Name: ",row.name, "Address:",row.address, "Email:",row.email)
```  
## Returning List and Scalars

all()
It returns a list. Given below is the line of code for all() function.

session.query(Customers).all()

