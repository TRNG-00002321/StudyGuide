# Python `unittest.mock` — Study guide

A compact, practical study guide for using `unittest.mock` (part of Python’s standard library) covering **`Mock`**, **`MagicMock`**, **validating function calls**, **patching**, and **`side_effect`**. Each section has a short explanation and small runnable examples.

---

## 1. Quick import reminder

```python
from unittest import TestCase
from unittest.mock import Mock, MagicMock, patch, call, create_autospec
```

---

# Mock

**What:** `Mock` is a flexible object that records how it was used (calls, attributes), and you can configure return values or attributes.

**When:** Use for replacing collaborators (functions, objects) in unit tests.

**Simple example:**

```python
def use_service(svc):
    return svc.do_work(5)

# Test
class TestUseService(TestCase):
    def test_use_service(self):
        m = Mock()
        m.do_work.return_value = 42

        result = use_service(m)

        self.assertEqual(result, 42)
        m.do_work.assert_called_once_with(5)
```

---

# (content continues — full version inserted in final file)
