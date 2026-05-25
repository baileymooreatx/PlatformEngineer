<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Type Hints in Python](#type-hints-in-python)
  - [Key Characteristics](#key-characteristics)
  - [Basic Syntax](#basic-syntax)
  - [Type Hints for Collections](#type-hints-for-collections)
  - [Union and Optional Types](#union-and-optional-types)
  - [Type Aliases](#type-aliases)
  - [Class Type Hints](#class-type-hints)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Type Hints in Python

Type hints in Python are a **syntactic feature** that allows developers to
specify the expected data types of variables, function parameters, and return
values. They were officially introduced in Python 3.5
via [PEP 484](https://peps.python.org/pep-0484/) to enhance code clarity and
support static analysis.

### Key Characteristics

- **Optional and Non-Enforced**: Python does not enforce type hints at runtime.
  The interpreter ignores them, so incorrect types won't cause runtime errors.
- **Static Analysis Tool Support**: Tools like `mypy`, `pyright`, or IDEs use
  type hints to catch potential bugs before execution.
- **Improved Code Readability**: Type hints serve as inline documentation,
  making it easier for developers to understand function signatures and variable
  usage.

### Basic Syntax

You add type hints using a colon (`:`) after a variable or parameter, and use
`->` to indicate the return type of a function.

```python
def greet(name: str) -> str:
    return f"Hello, {name}"


age: int = 25
```

In this example:

- `name: str` indicates that `name` should be a string.
- `-> str` specifies that the function returns a string.
- `age: int` declares that `age` is intended to be an integer.

Even if you pass an incorrect type (e.g., `greet(123)`), the code will still
run, but a type checker like `mypy` will flag it as an error.

### Type Hints for Collections

As of Python 3.9, built-in collection types can be used directly for type hints.
Prior versions require importing from the `typing` module.

```python
# Python 3.9+
users: list[str] = ["Alice", "Bob"]
scores: dict[str, int] = {"Alice": 95, "Bob": 87}

# For older versions (requires import)
from typing import List, Dict

users: List[str] = ["Alice", "Bob"]
scores: Dict[str, int] = {"Alice": 95, "Bob": 87}
```

### Union and Optional Types

Use `Union` when a value can be one of several types. In Python 3.10+, you can
use the `|` operator instead.

```python
# Python 3.10+
def add(x: int | float, y: int | float) -> int | float:
    return x + y


# Or with Optional (equivalent to Union[T, None])
def find_user(user_id: int) -> str | None:
    return "User" if user_id > 0 else None
```

For earlier versions:

```python
from typing import Union, Optional


def add(x: Union[int, float], y: Union[int, float]) -> Union[int, float]:
    return x + y


def find_user(user_id: int) -> Optional[str]:
    return "User" if user_id > 0 else None
```

### Type Aliases

You can create aliases for complex types to improve readability.

```python
from typing import Union

Number = Union[int, float]


def add(a: Number, b: Number) -> Number:
    return a + b
```

### Class Type Hints

Classes can be used directly as type hints.

```python
class Person:
    def __init__(self, name: str):
        self.name = name


def greet_person(person: Person) -> str:
    return f"Hello, {person.name}"
```
