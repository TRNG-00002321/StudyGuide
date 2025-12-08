# unittest — Unit testing framework
The unittest unit testing framework was originally inspired by JUnit and has a similar flavor as major unit testing frameworks in other languages. It supports test automation, sharing of setup and shutdown code for tests, aggregation of tests into collections, and independence of the tests from the reporting framework.

To achieve this, unittest supports some important concepts in an object-oriented way:

- **test fixture -** A test fixture represents the preparation needed to perform one or more tests, and any associated cleanup actions. This may involve, for example, creating temporary or proxy databases, directories, or starting a server process.
- **test case -** A test case is the individual unit of testing. It checks for a specific response to a particular set of inputs. unittest provides a base class, TestCase, which may be used to create new test cases.
- **test suite -** A test suite is a collection of test cases, test suites, or both. It is used to aggregate tests that should be executed together.
- **test runner -** A test runner is a component which orchestrates the execution of tests and provides the outcome to the user. The runner may use a graphical interface, a textual interface, or return a special value to indicate the results of executing the tests.

### Basic example
The unittest module provides a rich set of tools for constructing and running tests.
```python
import unittest

class TestStringMethods(unittest.TestCase):

    def test_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')

    def test_isupper(self):
        self.assertTrue('FOO'.isupper())
        self.assertFalse('Foo'.isupper())

    def test_split(self):
        s = 'hello world'
        self.assertEqual(s.split(), ['hello', 'world'])
        # check that s.split fails when the separator is not a string
        with self.assertRaises(TypeError):
            s.split(2)

if __name__ == '__main__':
    unittest.main()
```  
- A `test case` is created by subclassing `unittest.TestCase`. The three individual tests are defined with methods whose names start with the letters `test`. This naming convention informs the test runner about which methods represent tests.
- The crux of each test is a call to `assertEqual()` to check for an expected result; assertTrue() or assertFalse() to verify a condition; or assertRaises() to verify that a specific exception gets raised. These methods are used instead of the assert statement so the test runner can accumulate all test results and produce a report.
- The `setUp()` and `tearDown()` methods allow you to define instructions that will be executed before and after each test method. They are covered in more detail in the section Organizing test code.
- The final block shows a simple way to run the tests. unittest.main() provides a command-line interface to the test script. 
- You can run tests with more detail (higher verbosity) by passing in the -v flag:  
`python -m unittest -v test_module`

## Command-Line Interface
The unittest module can be used from the command line to run tests from modules, classes or even individual test methods:
```python
python -m unittest test_module1 test_module2
python -m unittest test_module.TestClass
python -m unittest test_module.TestClass.test_method
```

## Test Discovery
Unittest supports simple test discovery. In order to be compatible with test discovery, all of the test files must be modules or packages importable from the top-level directory of the project.  
`cd project_directory`  
`python -m unittest discover`

The discover sub-command has the following options:
- **-v, --verbose :** Verbose output
- **-s, --start-directory directory :** Directory to start discovery (. default)
- **-p, --pattern pattern :** Pattern to match test files (test*.py default)
- **-t, --top-level-directory directory :** Top level directory of project (defaults to start directory)  

## Organizing test code
The basic building blocks of unit testing are test cases, single scenarios that must be set up and checked for correctness. In unittest, test cases are represented by unittest.TestCase instances. To make your own test cases you must write subclasses of TestCase.
In order to test something, we use one of the assert* methods provided by the TestCase base class. If the test fails, an exception will be raised with an explanatory message, and unittest will identify the test case as a failure. Any other exceptions will be treated as errors.  
Python's unittest module provides several **fixture** methods within a TestCase class to set up and tear down resources for your tests. These methods allow you to prepare the testing environment before tests run and clean it up afterward, ensuring consistent and isolated test execution.

- **setUp():**  
    - This method is automatically called before each individual test method within a test case class.
    - It is used to prepare the test environment or create common resources needed by multiple tests.
    - Examples: initializing objects, establishing database connections, creating temporary files.
- **tearDown():**
    - This method is automatically called after each individual test method within a test case class.
    - It is used to clean up resources or reset the environment after a test has completed.
    - Examples: closing database connections, deleting temporary files, resetting mocked objects.
- **setUpClass(cls):** 
    - This class method is executed once before any test methods in the TestCase class are run. 
    - It's suitable for setting up resources that are expensive to create and can be shared across all tests in the class, such as database connections or loading large datasets.
- **tearDownClass(cls):** 
    - This class method is executed once after all test methods in the TestCase class have completed. 
    - It's used to clean up resources initialized in setUpClass.
***Example***
```python
# calculator.py
class Calculator:
    def add(self, a, b):
        return a + b

    def subtract(self, a, b):
        return a - b
```  
```python
# test_calculator.py
import unittest
from calculator import Calculator

class TestCalculator(unittest.TestCase):

    def setUp(self):
        """Set up a new Calculator instance before each test."""
        self.calc = Calculator()
        print("setUp called: Calculator instance created.")

    def tearDown(self):
        """Clean up resources after each test (optional for simple objects)."""
        # For more complex objects, you might reset attributes or close connections.
        self.calc = None # Explicitly dereference for clarity, though not strictly necessary for simple objects.
        print("tearDown called: Calculator instance cleaned up.")

    def test_add_positive_numbers(self):
        """Test adding two positive numbers."""
        result = self.calc.add(5, 3)
        self.assertEqual(result, 8)
        print("  test_add_positive_numbers executed.")

    def test_subtract_numbers(self):
        """Test subtracting numbers."""
        result = self.calc.subtract(10, 4)
        self.assertEqual(result, 6)
        print("  test_subtract_numbers executed.")

if __name__ == '__main__':
    unittest.main()
```
Execute using the following command `python -m unittest -v test_calculator.py`  

## Skipping tests and expected failures
The Python unittest framework provides mechanisms for handling tests that should not be run under certain conditions (skipping) or tests that are known to fail but are still included in the test suite (expected failures).
### Skipping Tests
Tests can be skipped using decorators or by raising a SkipTest exception.
- **@unittest.skip(reason):** This decorator unconditionally skips the decorated test method or class. A reason string explaining why the test is being skipped is required.
```python
    import unittest

    class MyTests(unittest.TestCase):
        @unittest.skip("Demonstrating unconditional skipping")
        def test_unconditional_skip(self):
            self.fail("This test should not run")
```
- **@unittest.skipIf(condition, reason):** This decorator skips the test if the condition evaluates to True
```python
    import unittest
    import sys

    class MyTests(unittest.TestCase):
        @unittest.skipIf(sys.platform == 'win32', "Skipping on Windows")
        def test_linux_only_feature(self):
            self.assertTrue(True) # This test runs only on non-Windows platforms
```
- **@unittest.skipUnless(condition, reason):** This decorator skips the test unless the condition evaluates to True. 
```python
    import unittest

    class MyTests(unittest.TestCase):
        @unittest.skipUnless(hasattr(self, 'resource_available'), "Resource not available")
        def test_requires_resource(self):
            self.assertTrue(True) # This test runs only if 'resource_available' exists
```
- **self.skipTest(reason):** This method can be called inside a test method to skip the test dynamically based on runtime conditions.
```python
    import unittest

    class MyTests(unittest.TestCase):
        def test_dynamic_skip(self):
            if not some_condition_is_met():
                self.skipTest("Condition not met for this test")
            self.assertTrue(True)
```

### Expected Failures
- **@unittest.expectedFailure:** This decorator marks a test as an expected failure. If the decorated test fails when run, it is not counted as a failure in the test report but as an "expected failure" (marked with an 'x'). If the test unexpectedly passes, it is reported as an error. This is useful for tests related to known bugs that are yet to be fixed.
```python
    import unittest

    class MyTests(unittest.TestCase):
        @unittest.expectedFailure
        def test_known_bug(self):
            self.assertEqual(1, 2, "This test is expected to fail due to a known bug")
```
## Grouping tests
**class unittest.TestSuite(tests=()) :** This class represents an aggregation of individual test cases and test suites. The class presents the interface needed by the test runner to allow it to be run as any other test case. Running a TestSuite instance is the same as iterating over the suite, running each test individually.
```python
   #my_module.py
    import unittest

    class MyFeatureTests(unittest.TestCase):
        # Test methods for 'MyFeature'
        def test_function_a(self):
            # ... assertions ...
            pass

        def test_function_b(self):
            # ... assertions ...
            pass

    class AnotherFeatureTests(unittest.TestCase):
        # Test methods for 'AnotherFeature'
        def test_function_c(self):
            # ... assertions ...
            pass

#     python -m unittest my_module.MyFeatureTests
```   
```python
    import unittest

    # Assuming MyFeatureTests and AnotherFeatureTests are defined as above
    suite = unittest.TestSuite()
        # Add all tests from MyFeatureTests
    suite.addTest(unittest.makeSuite(MyFeatureTests))

    # Add a specific test method from AnotherFeatureTests
    suite.addTest(AnotherFeatureTests('test_function_c'))
        runner = unittest.TextTestRunner()
    runner.run(suite)

# python -m unittest
```

## Testing Exceptions
In Python's unittest framework, the assertRaises method within a TestCase subclass is used to test whether a specific exception is raised by a function or a block of code
```python
import unittest

def divide(a, b):
    if b == 0:
        raise ZeroDivisionError("Cannot divide by zero")
    return a / b

class TestDivision(unittest.TestCase):
    def test_divide_by_zero(self):
        with self.assertRaises(ZeroDivisionError):
            divide(10, 0)
```  
```python
import unittest

def divide(a, b):
    if b == 0:
        raise ZeroDivisionError("Cannot divide by zero")
    return a / b

class TestDivision(unittest.TestCase):
    def test_divide_by_zero_message(self):
        with self.assertRaises(ZeroDivisionError) as cm:
            divide(10, 0)
        self.assertEqual(str(cm.exception), "Cannot divide by zero")
```

## Loading Test Data
Loading test data in Python unit tests, especially with the unittest framework, often involves reading data from external files or generating it programmatically within the test setup.
