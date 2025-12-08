# Pytest 
Pytest is a testing framework for Python that makes it easy to write simple and scalable test cases. It offers features like fixtures, parameterized tests, and detailed error reporting. With Pytest, you can efficiently test your code and ensure its reliability.

### Pytest Features
- **Simple Syntax** : Pytest uses a simple syntax for writing tests, making it easy to get started and understand test cases.
- **Fixtures** : Provides a powerful fixture mechanism to set up and tear down resources needed for tests, promoting code reuse and reducing duplication.
- **Parameterized Tests** : Supports parameterized tests, allowing you to run the same test with different inputs efficiently.
- **Detailed Reporting**: Offers detailed and readable test reports with clear information on test failures and errors, helping you diagnose issues quickly.
- **Extensible** : Highly extensible with plugins, enabling additional functionalities and integrations modified to your testing needs.  

### Pytest - Environment Setup
To install the latest version of pytest, execute the following command −  
`pip install pytest`  
Confirm the installation using the following command to display the help section of pytest.  
`pytest -h` 
### Identifying Test files and Test Functions
- Running pytest without mentioning a filename will run all files of format `**test_*.py**` or `*_test.py` in the current directory and subdirectories.
- Pytest automatically identifies those files as test files. We can make pytest run other filenames by explicitly mentioning them.
- Pytest requires the test function names to start with `**test**`.
- Function names which are not of format test* are not considered as test functions by pytest. We cannot explicitly make pytest consider any function not starting with test as a test function.

### Pytest - Writing Basic Test
Create a file named test_square.py
```python
import math

def test_sqrt():
   num = 25
   assert math.sqrt(num) == 5

def testsquare():
   num = 7
   assert 7*7 == 40

def tesequality():
   assert 10 == 11
```  
### Executing Tests
- Run the test using the following command −  
`pytest`  
***NOTE*** :  <mark>The function tesequality is not executed because pytest will not consider it as a test since its name is not of the format `test*.`</mark>  
** To increases the verbosity **
`pytest -v`  
***Note*** − <mark>pytest command will execute all the files of format `test_*` or `*_test` in the current directory and subdirectories.</mark>

- To execute the tests from a specific file, use the following syntax −  
`pytest <filename> -v`  
***Example:***  
`pytest test_compare.py -v`  
- Matching of Test Names
To execute the tests containing a string in its name we can use the following syntax −  
`pytest -k <substring> -v`  
-k <substring> represents the substring to search for in the test names.  
***Example :***   
`pytest -k check -v`  
This will execute all the test names having the word `check` in its name.  
```python
def test_check_greater():
   num = 100
   assert num > 100

def test_check_greater_equal():
   num = 100
   assert num >= 100

def test_less():
   num = 100
   assert num < 200
```  
### Pytest - Grouping the Tests
- Pytest allows us to use markers on test functions. 
- Markers are used to set various features/attributes to test functions. 
- Pytest provides many inbuilt markers such as xfail, skip and parametrize. 
- Users can create their own marker names. 

Markers are applied on the tests using the syntax given below   
`@pytest.mark.<markername>`  
To use markers, we have to import pytest module in the test file.  
We can define our own marker names to the tests and run the tests having those marker names.

To run the marked tests, we can use the following syntax −  
`pytest -m <markername> -v`
***test_compare.py***
```python
import pytest
@pytest.mark.great
def test_greater():
   num = 100
   assert num > 100

@pytest.mark.great
def test_greater_equal():
   num = 100
   assert num >= 100

@pytest.mark.others
def test_less():
   num = 100
   assert num < 200
```   
***test_square.py***
```python
import pytest
import math

@pytest.mark.square
def test_sqrt():
   num = 25
   assert math.sqrt(num) == 5

@pytest.mark.square
def testsquare():
   num = 7
   assert 7*7 == 40

@pytest.mark.others
   def test_equality():
   assert 10 == 11
```  
To run the tests marked as others, run the following command −  
`pytest -m others -v`  

### Pytest - Fixtures
Pytest fixtures are a powerful mechanism for setting up and tearing down resources or test data required for testing in pytest. They are essentially functions decorated with `@pytest.fixture` that provide a return value or perform setup/teardown actions for tests.  
**Characteristics and uses of pytest fixtures:**
- **Setup and Teardown:** Fixtures can encapsulate the setup logic (e.g., creating a database connection, initializing an object) before a test runs and optionally include teardown logic (e.g., closing a connection, cleaning up temporary files) after the test. The teardown is typically handled using a `yield` statement within the fixture, where ***code before yield is setup*** and ***code after yield is teardown***.  
- **Reusability:** Fixtures promote code reuse by allowing you to define setup routines once and then use them across multiple test functions, classes, or modules without duplicating the setup code within each test.
- **Dependency Injection:** Tests or other fixtures can "request" a fixture by including its name as a parameter in their function signature. pytest automatically injects the return value of the fixture into the requesting function.
- **Scoping:** Fixtures can be defined with different scopes (function, class, module, session) to control how often they are executed. For example, a session-scoped fixture runs once per test session, while a function-scoped fixture runs before each test function.
- **Parametrization:** Fixtures can be parameterized to provide a sequence of different values to tests, allowing you to run the same test logic with various inputs.
- **Built-in Fixtures:** pytest provides several useful built-in fixtures, such as tmpdir (for temporary directories), capsys (for capturing stdout/stderr), and monkeypatch (for modifying objects during testing).

```python
import pytest

@pytest.fixture
def resource_fixture():
    print("\nSetting up resource...")
    resource = "my_shared_resource"
    yield resource  # The value 'resource' is yielded to the test function
    print("Tearing down resource...")

def test_using_resource(resource_fixture):
    print(f"Test is using: {resource_fixture}")
    assert resource_fixture == "my_shared_resource"

# OUTPUT
Setting up resource...
Test is using: my_shared_resource
Tearing down resource...
```  
***Note :-*** <mark>Running pytest with the -s flag (short for --capture=no) will disable pytest's output capturing, allowing all print statements to be displayed in real-time as they are executed.
***pytest -s your_test_file.py***</mark>

### Pytest - Conftest.py
The `conftest.py` file is a special file used in the pytest testing framework in Python. Its primary purpose is to provide a mechanism for sharing fixtures, hooks, and local plugins across multiple test files within a project.
- **Shared Fixtures:** Fixtures defined in a conftest.py file are automatically discovered by pytest and can be used by any test function or test class within the same directory or any subdirectory within the conftest.py's scope. This eliminates the need to import fixtures explicitly in each test file, promoting reusability and reducing boilerplate code.
- **Hooks and Custom Configuration:** conftest.py can also be used to implement custom pytest hooks. Hooks are functions that allow you to modify or extend the behavior of pytest during various stages of the test execution process, such as test collection, setup, teardown, and reporting.
- **Local Plugins:** You can use conftest.py to define local plugins specific to your project or a particular test directory. This allows for customized behavior and extensions tailored to your testing needs.
**How Conftest.py works:**
When pytest discovers tests, it automatically searches for `conftest.py` files in the test directory and its parent directories. Fixtures and hooks defined in these files become available to the tests within their respective scopes. The scope of a conftest.py file extends to all subdirectories within its parent directory. If multiple conftest.py files exist in a nested directory structure, fixtures and hooks from parent conftest.py files are also available to tests in child directories.
***Example***
```python
# conftest.py
import pytest

@pytest.fixture
def my_fixture():
    print("\nSetting up my_fixture")
    yield "fixture_data"
    print("Tearing down my_fixture")

# test_example.py
def test_using_fixture(my_fixture):
    assert my_fixture == "fixture_data"
``` 
In the above example, my_fixture is defined in conftest.py and can be directly used as an argument in test_using_fixture in test_example.py without any explicit imports.

### Pytest - Parameterizing Tests
Pytest offers powerful features for parameterizing tests, allowing a single test function to be executed with multiple sets of input data. This reduces code duplication and improves test coverage.  
We can do this by using the following marker −  
`@pytest.mark.parametrize`
***Example***
```python
    import pytest

    @pytest.mark.parametrize("input_value, expected_output", [
        (1, 2),
        (2, 4),
        (3, 6),
    ])
    def test_double(input_value, expected_output):
        assert input_value * 2 == expected_output
```  
***Example***
```python
import pytest

# Assume you have a function to test, for example:
def add(a, b):
    return a + b

# Parameterized test for the 'add' function
@pytest.mark.parametrize(
    "num1, num2, expected_sum",  # Names of the parameters to be passed to the test function
    [
        (1, 2, 3),        # Test case 1: num1=1, num2=2, expected_sum=3
        (0, 0, 0),        # Test case 2: num1=0, num2=0, expected_sum=0
        (-1, 5, 2),       # Test case 3: num1=-1, num2=5, expected_sum=4
        (10, -3, 7),      # Test case 4: num1=10, num2=-3, expected_sum=7
        (2.5, 3.5, 6.0),  # Test case 5: num1=2.5, num2=3.5, expected_sum=6.0
    ]
)
def test_add_function(num1, num2, expected_sum):
    """
    Tests the 'add' function with various inputs.
    """
    result = add(num1, num2)
    assert result == expected_sum
```
### Pytest - Xfail/Skip Tests
Pytest provides mechanisms to manage tests that are not expected to pass or are not relevant under certain conditions, using `@pytest.mark.skip, @pytest.mark.skipif, and @pytest.mark.xfail.`  

**Skipping Tests:**  
`@pytest.mark.skip(reason="..."):` This decorator completely prevents a test function from being executed. It is useful when a test is temporarily irrelevant, or a specific feature is not yet implemented.
```python
import pytest
  @pytest.mark.skip(reason="This feature is under development")
    def test_new_feature():
        assert False 
```  
`@pytest.mark.skipif(condition, reason="..."):` This decorator skips a test if a specified condition evaluates to True. This is particularly useful for skipping tests based on environmental factors (e.g., operating system, Python version, installed libraries).
```Python
import pytest
import sys

@pytest.mark.skipif(sys.platform != "win32", reason="Requires Windows")
def test_windows_only_functionality():
   assert True
```  
**XFailing Tests**
`@pytest.mark.xfail(reason="...", strict=False):` This decorator marks a test as "expected to fail." The test is still executed, but if it fails, it is reported as XFAIL (xfailed) instead of FAILED. If an xfail test unexpectedly passes, it is reported as XPASS (xpassed) by default (when strict=False). If strict=True, an xfail test passing unexpectedly will be reported as FAILED.
```Python
import pytest
@pytest.mark.xfail(reason="Known bug, fix pending")
def test_buggy_function():
    assert 1 == 2 # This test is expected to fail
```  
### Test Execution Results in XML Format
To generate Pytest test execution results in XML format, specifically in the widely recognized JUnit XML format, you can utilize the --junitxml flag when running your tests.  
`pytest --junitxml=test_results.xml`