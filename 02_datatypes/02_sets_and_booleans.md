# Python Sets & Booleans — Study Notes 🐍
> Based on hands-on REPL practice | Python 3.12

---

## 1. Sets

A **set** is an **unordered collection of unique elements**, written with curly braces `{}`.

```python
setOne = {1, 2, 3, 4}
```

> **Note:** Sets do **not** allow duplicates and have **no guaranteed order**.

---

### Set Operations

Sets support mathematical operations directly with operators:

| Operation | Operator | Example | Result |
|---|---|---|---|
| Intersection | `&` | `{1,2,3,4} & {1,3}` | `{1, 3}` |
| Union | `\|` | `{1,2,3,4} \| {1,3,7}` | `{1, 2, 3, 4, 7}` |
| Difference | `-` | `{1,2,3,4} - {1,2,3,4}` | `set()` |

```python
setOne & {1, 3}       # {1, 3}       → elements common to both
setOne | {1, 3, 7}    # {1, 2, 3, 4, 7} → all elements from both (no duplicates)
setOne - {1, 2, 3, 4} # set()        → elements in setOne but NOT in the other
```

> **Key Point:** Sets are **immutable in content during operations** — `setOne` itself stays unchanged unless you reassign.

---

### Empty Set vs Empty Dict

```python
type({})    # <class 'dict'>  ← {} alone creates a dict, NOT a set!
```

To create an **empty set**, you must use:
```python
empty_set = set()   # ✓ correct
empty_set = {}      # ✗ this is an empty dictionary!
```

---

## 2. Booleans

```python
type(True)    # <class 'bool'>
```

In Python, `bool` is a **subclass of `int`**.

---

### Booleans are Integers Under the Hood

```python
True  == 1    # True
False == 0    # True

True  + 4     # 5   → True is treated as 1
False + 4     # 4   → False is treated as 0
```

This works because `True = 1` and `False = 0` at the integer level.

---

### `==` vs `is` — An Important Distinction

```python
True == 1     # True  ✓ → checks VALUE equality
True is 1     # False ⚠️ → checks IDENTITY (same object in memory)
```

Running `True is 1` also gives a **SyntaxWarning**:
```
SyntaxWarning: "is" with 'int' literal. Did you mean "=="?
```

| Operator | Checks | Use for |
|---|---|---|
| `==` | Value equality | Comparing values |
| `is` | Identity (same object) | Checking `None`, singletons |

> **Rule of thumb:** Always use `==` to compare values. Use `is` only for `None` checks like `if x is None`.

---

## 🧠 Quick Recap

| Concept | Key Takeaway |
|---|---|
| `{}` | Creates a **dict**, not a set |
| `set()` | Creates an empty set |
| `&`, `\|`, `-` | Intersection, Union, Difference |
| `True == 1` | `True` (bool is a subclass of int) |
| `True is 1` | `False` (different objects in memory) |
| `True + 4` | `5` (bool arithmetic works!) |

---

*Keep practicing! 🚀*
