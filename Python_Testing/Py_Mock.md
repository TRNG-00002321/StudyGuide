# pytest-mock
**pytest-mock** is a plugin for the popular Python testing framework pytest that provides easy access to mocking capabilities. It builds on top of Python's built-in unittest, simplifying the process of mocking during testing.  
pytest-mock enhances readability and makes it easy to implement mocks in tests with a more pytest-native approach. Whether you need to mock individual functions, class methods, or entire objects, pytest-mock provides the flexibility needed for effective testing without the extra complexity.  

### Installing pytest and pytest-mock
```python
pip install pytest
pip install pytest-mock
```
## Mocking with pytest-mock
A mock object simulates the behavior of a real object. It is often used in unit tests to isolate components and test their behavior without executing dependent code.  
***For example***, you might use a mock object to simulate a database call without actually connecting to the database.  
Mocking is particularly useful when the real object:
- Is difficult to create or configure.
- Is time-consuming to use (e.g., accessing a remote database).
- Has side effects that should be avoided during testing (e.g., sending emails, incurring costs).  
### Using the mocker fixture
pytest-mock provides a mocker fixture, making creating and controlling mock objects easy. The mocker fixture is powerful and integrates into your pytest tests.  
<mark>**What are fixtures?** 
In Python, fixtures are reusable components that set up and tear down resources needed for tests, such as databases or files. They ensure consistency, reduce duplication, and simplify test setup.</mark>

```python
def fetch_weather_data(api_client):
    response = api_client.get("https://api.open-meteo.com/v1/forecast?latitude=52.52&longitude=13.41&current=temperature")
    if response.status_code == 200:
        return response.json()
    else:
        return None
```
The fetch_weather_data  function depends on an external weather API to retrieve data, but calling the API during tests could incur unnecessary costs.   
To avoid this, you can use mocking to simulate the API's behavior in your tests, ensuring the application is tested without making external calls.
```python
from withoutmock.fetchwether import fetch_weather_data


def test_fetch_weather_data(mocker):
    # Create a mock API client
    mock_api_client = mocker.Mock()

    # Mock the response of the API client
    mock_response = mocker.Mock()
    mock_response.status_code = 200
    mock_response.json.return_value = {"temperature": "20C", "condition": "Sunny"}

    # Set the mock API client to return the mocked response
    mock_api_client.get.return_value = mock_response

    # Call the function with the mock API client
    result = fetch_weather_data(mock_api_client)

    # Assert that the correct data is returned
    assert result == {"temperature": "20C", "condition": "Sunny"}

    mock_api_client.get.assert_called_once_with("https://api.open-meteo.com/v1/forecast?latitude=52.52&longitude=13.41&current=temperature")
```
### Mocking functions or class methods
You may need to test a function that depends on other functions or methods, but you want to control their behavior during testing. Mocking allows you to replace those dependencies with predefined behavior:
```python
# production code
def calculate_discount(price, discount_provider):
    discount = discount_provider.get_discount()
    return price - (price * discount / 100)

# test code
def test_calculate_discount(mocker):
    # Mock the get_discount method
    mock_discount_provider = mocker.Mock()
    mock_discount_provider.get_discount.return_value = 10  # Mocked discount value
    # Call the function with the mocked dependency
    result = calculate_discount(100, mock_discount_provider)
    # Assert the calculated discount is correct
    assert result == 90
    mock_discount_provider.get_discount.assert_called_once()
```

## Mock and MagicMock
- **Mock :** A Mock object is a flexible stand-in for other objects. It records how it's used (calls, attribute access) and allows you to define return values or side effects for its methods and attributes.

- **MagicMock :** MagicMock is a subclass of Mock that automatically implements all of Python's "magic methods" (like `__len__`, `__str__`, `__getitem__`, etc.). This makes it more suitable for mocking objects that are expected to behave like built-in types or custom classes with special methods.

```python
# my_collection.py
class MyCollection:
    def __init__(self, items):
        self._items = list(items)

    def __len__(self):
        return len(self._items)

    def __getitem__(self, index):
        return self._items[index]

# test_my_collection.py
def test_my_collection_len_and_getitem(mocker):
    mock_collection = mocker.MagicMock(spec=my_collection.MyCollection)
    mock_collection.__len__.return_value = 5
    mock_collection.__getitem__.side_effect = lambda i: f"item_{i}"

    assert len(mock_collection) == 5
    assert mock_collection[2] == "item_2"
    mock_collection.__len__.assert_called_once()
    mock_collection.__getitem__.assert_called_once_with(2)
```

## Patching in pytest-mock
Patching in pytest-mock involves temporarily replacing an object (like a function, method, or class) with a mock object during a test. This is useful for isolating the code under test from its dependencies, especially when those dependencies are slow, involve external resources (like network calls or databases), or have unpredictable behavior. pytest-mock provides the mocker fixture, which is a wrapper around unittest.mock, simplifying the process of creating and managing mocks within your Pytest tests.  
**How patching works:**  
The mocker.patch() method replaces the target object with a MagicMock instance (or a custom mock object if specified). When the test finishes, the original object is automatically restored, ensuring that your tests don't permanently alter the program's state.
```python
# my_module.py
import requests

def get_user_data(user_id):
    response = requests.get(f"https://api.example.com/users/{user_id}")
    response.raise_for_status()
    return response.json()
```  
```python
# test_my_module.py
import pytest
from my_module import get_user_data

def test_get_user_data(mocker):
    # Create a mock response object
    mock_response = mocker.Mock()
    mock_response.json.return_value = {"id": 1, "name": "Test User"}
    mock_response.raise_for_status.return_value = None  # No error

    # Patch requests.get to return our mock response
    mocker.patch("my_module.requests.get", return_value=mock_response)

    # Call the function under test
    user_data = get_user_data(1)

    # Assertions
    assert user_data == {"id": 1, "name": "Test User"}
    #mocker.patch.call_args_list[0].args[0] == "https://api.example.com/users/1" # Check the URL
```
## Side Effects in pytest-mock
In pytest-mock, which utilizes unittest.mock's MagicMock objects, the **side_effect** attribute allows you to define custom behavior for a mocked object when it is called. This is particularly useful when you need the mock to do more than simply return a fixed value, such as raising an exception, returning different values across multiple calls, or executing specific logic.
**Types of side_effect:**
- **Iterable:** You can assign an iterable (like a list or a generator) to side_effect. Each time the mock is called, it will return the next item from the iterable. If an item is an exception instance, that exception will be raised.
- **Callable:** You can assign a function or a lambda to side_effect. This function will be called with the same arguments as the mock, and its return value will be used as the mock's return value (unless the function returns mock.DEFAULT, in which case return_value is used). 
- **Exception:** You can assign an exception class or instance directly to side_effect. Each time the mock is called, that exception will be raised.

***Example:***
Consider a function fetch_data_from_api that makes an API call and might encounter network errors or return different data based on the call.
```python
# my_module.py
import requests

def fetch_data_from_api(url):
    try:
        response = requests.get(url)
        response.raise_for_status()  # Raise an exception for bad status codes
        return response.json()
    except requests.exceptions.RequestException as e:
        print(f"Error fetching data: {e}")
        return None
```  
***let's test this with pytest-mock using side_effect***
```python
# test_my_module.py
import pytest
from unittest import mock
from my_module import fetch_data_from_api

def test_fetch_data_success_multiple_calls(mocker):
    # Mock requests.get to return different responses on successive calls
    mock_response_1 = mocker.MagicMock()
    mock_response_1.json.return_value = {"data": "first"}
    mock_response_1.raise_for_status.return_value = None

    mock_response_2 = mocker.MagicMock()
    mock_response_2.json.return_value = {"data": "second"}
    mock_response_2.raise_for_status.return_value = None

    mocker.patch('my_module.requests.get', side_effect=[mock_response_1, mock_response_2])

    assert fetch_data_from_api("http://example.com/api/1") == {"data": "first"}
    assert fetch_data_from_api("http://example.com/api/2") == {"data": "second"}

def test_fetch_data_network_error(mocker):
    # Mock requests.get to raise an exception
    mocker.patch('my_module.requests.get', side_effect=requests.exceptions.ConnectionError("Network down"))

    assert fetch_data_from_api("http://example.com/api/fail") is None

def test_fetch_data_custom_logic(mocker):
    def custom_get_behavior(url, *args, **kwargs):
        if "success" in url:
            mock_resp = mocker.MagicMock()
            mock_resp.json.return_value = {"status": "ok"}
            mock_resp.raise_for_status.return_value = None
            return mock_resp
        else:
            raise requests.exceptions.HTTPError("404 Not Found")

    mocker.patch('my_module.requests.get', side_effect=custom_get_behavior)

    assert fetch_data_from_api("http://example.com/api/success") == {"status": "ok"}
    assert fetch_data_from_api("http://example.com/api/error") is None
```

