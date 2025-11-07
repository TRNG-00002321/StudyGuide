# Pandas

## What is Pandas?  
Pandas is a Python library used for working with data sets.
It has functions for analyzing, cleaning, exploring, and manipulating data.
The name "Pandas" has a reference to both "Panel Data", and "Python Data Analysis" and was created by Wes McKinney in 2008.

**Why Use Pandas?**  
Pandas allows us to analyze big data and make conclusions based on statistical theories.
Pandas can clean messy data sets, and make them readable and relevant.
Relevant data is very important in data science.

`Data Science: is a branch of computer science where we study how to store, use and analyze data for deriving information from it.`

**What Can Pandas Do?**  
Pandas gives you answers about the data. Like:

- Is there a correlation between two or more columns?
- What is average value?
- Max value?
- Min value?
Pandas are also able to delete rows that are not relevant, or contains wrong values, like empty or NULL values. This is called cleaning the data.

**Installation of Pandas**  
If you have Python and PIP already installed on a system, then installation of Pandas is very easy.

Install it using this command:

`C:\Users\Your Name>pip install pandas`

**Import Pandas**  
Once Pandas is installed, import it in your applications by adding the import keyword:

`import pandas`

Now Pandas is imported and ready to use.

```python
import pandas
mydataset = {
  'cars': ["BMW", "Volvo", "Ford"],
  'passings': [3, 7, 2]
}
myvar = pandas.DataFrame(mydataset)
print(myvar)

#OUTPUT
    cars  passings
0    BMW         3
1  Volvo         7
2   Ford         2
```
**Pandas is usually imported under the pd alias.**
```python
import pandas as pd
```

## Pandas Series
**What is a Series?**  
A Pandas Series is like a column in a table.
It is a one-dimensional array holding data of any type.  
_Create a simple Pandas Series from a list:_
```python
import pandas as pd
a = [1, 7, 2]
myvar = pd.Series(a)
print(myvar)
```

**Labels**  
If nothing else is specified, the values are labeled with their index number. First value has index 0, second value has index 1 etc.
This label can be used to access a specified value.  
_Return the first value of the Series:_
```python
print(myvar[0])
```  
**Create Labels**  
With the index argument, you can name your own labels.  
_Create your own labels:_
```python
import pandas as pd
a = [1, 7, 2]
myvar = pd.Series(a, index = ["x", "y", "z"])
print(myvar)
```  
**Key/Value Objects as Series**  
You can also use a key/value object, like a dictionary, when creating a Series.  
_Create a simple Pandas Series from a dictionary:_
```python
import pandas as pd
calories = {"day1": 420, "day2": 380, "day3": 390}
myvar = pd.Series(calories)
print(myvar)
```  
## Pandas DataFrames  
**What is a DataFrame?**  
A Pandas DataFrame is a 2 dimensional data structure, like a 2 dimensional array, or a table with rows and columns.

_Create a simple Pandas DataFrame:_
```python
import pandas as pd
data = {
  "calories": [420, 380, 390],
  "duration": [50, 40, 45]
}
#load data into a DataFrame object:
df = pd.DataFrame(data)
print(df) 
```  
**Locate Row**  
As you can see from the result above, the DataFrame is like a table with rows and columns.
Pandas use the loc attribute to return one or more specified row(s)  
_Return row 0:_ 
```python
#refer to the row index:
print(df.loc[0])
```  
**Named Indexes**  
With the index argument, you can name your own indexes.  
_Add a list of names to give each row a name:_
```python
import pandas as pd

data = {
  "calories": [420, 380, 390],
  "duration": [50, 40, 45]
}

df = pd.DataFrame(data, index = ["day1", "day2", "day3"])
print(df) 
```  
**Locate Named Indexes**  
Use the named index in the loc attribute to return the specified row(s).  
_Return "day2":_
```python
#refer to the named index:
print(df.loc["day2"])
```  
## Pandas Read CSV  
**Read CSV Files**  
A simple way to store big data sets is to use CSV files (comma separated files).
CSV files contains plain text and is a well know format that can be read by everyone including Pandas.  
_Load the CSV into a DataFrame:_
```python
import pandas as pd
df = pd.read_csv('data.csv')
print(df.to_string()) 
```  
> **Tip:** use `to_string()` to print the entire DataFrame.  
> If you have a large DataFrame with many rows, Pandas will only return the first 5 rows, and the last 5 rows  

**max_rows**  
The number of rows returned is defined in Pandas option settings.
You can check your system's maximum rows with the `pd.options.display.max_rows` statement.  
_Check the number of maximum returned rows:_
```python
import pandas as pd
print(pd.options.display.max_rows) 
```  
In my system the number is 60, which means that if the DataFrame contains more than 60 rows, the print(df) statement will return only the headers and the first and last 5 rows.  
You can change the maximum rows number with the same statement.  
_Increase the maximum number of rows to display the entire DataFrame:_
```python
import pandas as pd
pd.options.display.max_rows = 9999
df = pd.read_csv('data.csv')
print(df) 
```

## Read JSON  
Big data sets are often stored, or extracted as JSON.  
JSON is plain text, but has the format of an object, and is well known in the world of programming, including Pandas.  
_Load the JSON file into a DataFrame:_
```python
import pandas as pd
df = pd.read_json('data.json')
print(df.to_string()) 
```  
**Dictionary as JSON**  
> JSON = Python Dictionary  

JSON objects have the same format as Python dictionaries.  
If your JSON code is not in a file, but in a Python Dictionary, you can load it into a DataFrame directly:  
_Load a Python Dictionary into a DataFrame:_
```python
import pandas as pd

data = {
  "Duration":{
    "0":60,
    "1":60,
    "2":60,
    "3":45,
    "4":45,
    "5":60
  },
  "Pulse":{
    "0":110,
    "1":117,
    "2":103,
    "3":109,
    "4":117,
    "5":102
  },
  "Maxpulse":{
    "0":130,
    "1":145,
    "2":135,
    "3":175,
    "4":148,
    "5":127
  },
  "Calories":{
    "0":409,
    "1":479,
    "2":340,
    "3":282,
    "4":406,
    "5":300
  }
}

df = pd.DataFrame(data)

print(df) 
```

## Pandas - Analyzing DataFrames
**Viewing the Data**  
One of the most used method for getting a quick overview of the DataFrame, is the `head()` method.  
The `head()` method returns the headers and a specified number of rows, starting from the top.  
_Get a quick overview by printing the first 10 rows of the DataFrame:_
```python
import pandas as pd
df = pd.read_csv('data.csv')
print(df.head(10))
```

> Note: if the number of rows is not specified, the head() method will return the top 5 rows.

There is also a `tail()` method for viewing the last rows of the DataFrame.  
The `tail()` method returns the headers and a specified number of rows, starting from the bottom.    
The DataFrames object has a method called `info()`, that gives you more information about the data set.  

## Pandas - Cleaning Data  
**Data Cleaning**  
Data cleaning means fixing bad data in your data set.  
Bad data could be:
- Empty cells
- Data in wrong format
- Wrong data
- Duplicates

## Pandas - Cleaning Empty Cells  
**Empty Cells**  
Empty cells can potentially give you a wrong result when you analyze data.

**Remove Rows**  
One way to deal with empty cells is to remove rows that contain empty cells.  
This is usually OK, since data sets can be very big, and removing a few rows will not have a big impact on the result.

_Return a new Data Frame with no empty cells:_  
```python
import pandas as pd
df = pd.read_csv('data.csv')
new_df = df.dropna()
print(new_df.to_string())
``` 
> Note: By default, the dropna() method returns a new DataFrame, and will not change the original.

_Remove all rows with NULL values:_  
```python
import pandas as pd
df = pd.read_csv('data.csv')
df.dropna(inplace = True)
print(df.to_string())
```

## Pandas - Removing Duplicates  
**Discovering Duplicates**  
Duplicate rows are rows that have been registered more than one time.  
By taking a look at our test data set, we can assume that row 11 and 12 are duplicates.  
To discover duplicates, we can use the duplicated() method.  
The duplicated() method returns a Boolean values for each row:  
_Returns True for every row that is a duplicate, otherwise False:_  
`print(df.duplicated())`

**Removing Duplicates**  
To remove duplicates, use the drop_duplicates() method.  
_Remove all duplicates:_  
`df.drop_duplicates(inplace = True)`


