# Python `unittest.mock` — Study Guide

# Mock
`Mock`  is a substitute object used during unit testing that simulates the behavior of a real object or system dependency (like a database, API, or external service). Mocks allow developers to isolate the code being tested, control the environment, and verify interactions, without incurring the performance costs or side effects of the actual dependencies.Mocking in Python is primarily done using the unittest.mock library containing the `Mock` and `MagicMock` classes.

## Key features
- Records calls: `assert_called_with`, `call_args`, `call_args_list`.
- `return_value` controls what calling the mock returns.
- Attributes on a mock are mocks themselves (lazy creation).

## Example
```python
# test_mock_basic.py
import unittest
from unittest.mock import Mock

def greet(func):
    # expects func to be callable and return a string
    return "Hello, " + func()

class TestMockBasic(unittest.TestCase):
    def test_mock_return_value_and_assert_call(self):
        fake_func = Mock(return_value="World")
        result = greet(fake_func)

        # behavior check
        self.assertEqual(result, "Hello, World")

        # validation: was called once
        fake_func.assert_called_once()
        # validation: called with no arguments
        fake_func.assert_called_once_with()

if __name__ == "__main__":
    unittest.main()
```

---

# MagicMock
`MagicMock` is a subclass of `Mock` that pre-defines magic methods (`__len__`, `__iter__`, `__enter__`, etc.). Useful when you need mocks that work with protocols.

## Example
```python
# test_magicmock.py
import unittest
from unittest.mock import MagicMock

def use_context(cm):
    with cm as resource:
        return len(resource)

class TestMagicMock(unittest.TestCase):
    def test_magic_methods(self):
        resource_mock = MagicMock()
        # configure the object returned by __enter__
        resource_mock.__enter__.return_value = [1, 2, 3]
        # len() of the returned value should be 3
        self.assertEqual(use_context(resource_mock), 3)

    def test_len_magic(self):
        seq_mock = MagicMock()
        seq_mock.__len__.return_value = 5
        self.assertEqual(len(seq_mock), 5)

if __name__ == "__main__":
    unittest.main()
```

---

# Validating Function Calls
When testing, you often need to assert how a mocked function/object was called: number of calls, argument values, call order, or that specific calls happened (possibly in any order).
## Useful assertions
- `assert_called`, `assert_not_called`
- `assert_called_once`, `assert_called_once_with`
- `assert_called_with`
- `assert_any_call`
- `assert_has_calls`
- `call_args`, `call_args_list`

## Example
```python
# test_call_validation.py
import unittest
from unittest.mock import Mock, call

def process(items, worker):
    for i, item in enumerate(items):
        worker(item, index=i)
    worker("final", index="f")

class TestCallValidation(unittest.TestCase):
    def test_call_order_and_args(self):
        worker = Mock()
        process(["a", "b"], worker)

        # total calls = 3
        self.assertEqual(worker.call_count, 3)

        # check last call
        worker.assert_called_with("final", index="f")

        # check exact call list and order
        expected = [call("a", index=0), call("b", index=1), call("final", index="f")]
        worker.assert_has_calls(expected, any_order=False)

        # check a call exists (any order)
        worker.assert_any_call("b", index=1)

if __name__ == "__main__":
    unittest.main()
```

---

# patching
patch temporarily replaces a target object (module attribute, class, function) with a Mock (or provided object) during a test. It is commonly used to replace network calls, DB access, random functions, etc.

patch can be used as:
- A decorator (@patch('module.target'))
- A context manager (with patch('module.target') as mock:)
- Directly with patch.object(...) to patch attributes on objects.

Important: patch replaces where the object is looked up in code under test — usually the module that imports/uses it.
## Example
```python
# app.py
import requests
def fetch_user(user_id):
    resp = requests.get(f"https://api.example.com/users/{user_id}")
    return resp.json()
```

```python
# test_app.py
import unittest
from unittest.mock import patch, Mock
import app

class TestPatch(unittest.TestCase):
    @patch("app.requests.get")   # patch where requests.get is looked up (inside app)
    def test_fetch_user_with_patch_decorator(self, mock_get):
        fake_response = Mock()
        fake_response.json.return_value = {"id": 1, "name": "Alice"}
        mock_get.return_value = fake_response

        user = app.fetch_user(1)
        self.assertEqual(user["name"], "Alice")

        mock_get.assert_called_once_with("https://api.example.com/users/1")

    def test_patch_context_manager(self):
        with patch("app.requests.get") as mock_get:
            mock_get.return_value.json.return_value = {"id": 2}
            self.assertEqual(app.fetch_user(2), {"id": 2})
            mock_get.assert_called_once()

if __name__ == "__main__":
    unittest.main()
```

---

# side_effect
side_effect is an attribute on a Mock that defines additional behavior when the mock is called:
- If side_effect is a callable, it will be called with the same arguments as the mock; the mock call returns that callable's return value unless return_value is also set.
- If side_effect is an iterable, each call to the mock returns the next element from that iterable (useful to simulate sequence of responses). If an element is an exception instance or exception class, it will be raised on that call.
- If side_effect is set to an exception, that exception is raised whenever the mock is called.

## Example
```python
# test_side_effect.py
import unittest
from unittest.mock import Mock

def compute(a, b):
    return a + b

class TestSideEffects(unittest.TestCase):
    def test_side_effect_callable(self):
        m = Mock()
        # side_effect as a function: mimics real compute but logs or changes behavior
        m.side_effect = lambda a, b: a * b  # different behavior
        self.assertEqual(m(3, 4), 12)  # uses side_effect

    def test_side_effect_iterable(self):
        m = Mock(side_effect=[1, 2, 3])
        self.assertEqual(m(), 1)
        self.assertEqual(m(), 2)
        self.assertEqual(m(), 3)
        # next call will raise StopIteration (iterable exhausted) — be aware

    def test_side_effect_raises(self):
        m = Mock()
        m.side_effect = ValueError("boom")
        with self.assertRaises(ValueError):
            m(1, 2)

if __name__ == "__main__":
    unittest.main()
```

---

# Summary
- Use Mock for basic stubbing and call validation.
- Use MagicMock when magic methods/protocols are needed.
- Validate calls with `assert_*` helpers and `call_args_list`.
- Patch objects where they are imported.
- Use side_effect for dynamic behavior, cycling results, or raising errors.
