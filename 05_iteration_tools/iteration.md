# 🔁 Python Iteration Tools — Study Notes

> **Iteration** is the process of going through items one by one. Python uses the **iterator protocol** to do this consistently across files, lists, dicts, ranges, and more.

---

## 1. Reading Files with `readline()`

```python
f = open('hello.py')
f.readline()   # 'import time\n'
f.readline()   # '\n'
f.readline()   # 'print("I am sejal")\n'
```

- `open()` returns a **file object**.
- `readline()` reads **one line at a time**, including the `\n` newline character.
- When the file ends, `readline()` returns an **empty string `''`** (not an error).
- Calling `readline()` again after EOF keeps returning `''`.

> 💡 To re-read from the start, call `open()` again — the file pointer resets.

---

## 2. Files as Iterators — `__next__()`

```python
f = open('hello.py')
f.__next__()   # 'import time\n'
f.__next__()   # '\n'
# ...
f.__next__()   # StopIteration ← raised when file ends
```

- File objects are **iterators** — they implement `__next__()`.
- `__next__()` works just like `readline()`, but raises `StopIteration` at EOF instead of returning `''`.
- This is the same protocol used by `for` loops internally.

---

## 3. Looping Over a File with `for`

```python
# With default newline (double spacing)
for line in open('hello.py'):
    print(line)

# Clean output — suppress extra newline
for line in open('hello.py'):
    print(line, end="")
```

**Output:**
```
import time
print("I am sejal")
username = "sejal"
print(username)
```

- `for` loops call `__next__()` automatically behind the scenes.
- Each `line` already ends with `\n`, so use `end=""` to avoid double blank lines.

---

## 4. `while` Loop File Reading Pattern

```python
f = open('hello.py')
while True:
    line = f.readline()
    if not line: break        # empty string '' is falsy → stop
    print(line, end="")
```

- Classic pattern: read line by line, break when `readline()` returns `''`.
- `if not line` works because **empty string is falsy** in Python.

```python
# Falsy check demo
test = ""
if not test:
    print("hi")   # Output: hi

test = "sejal"
if not test:
    print("hi")   # No output — non-empty string is truthy
```

---

## 5. The Iterator Protocol

Every iterator in Python follows this contract:

| Method | What it does |
|--------|-------------|
| `iter(obj)` | Returns the iterator object |
| `next(obj)` or `obj.__next__()` | Returns the next item |
| `StopIteration` | Raised when items are exhausted |

> `next()` is the clean, Pythonic way. `__next__()` is the underlying dunder method — both do the same thing.

---

## 6. Lists vs Files — `iter()` Behavior

```python
myList = [1, 2, 3, 4]
I = iter(myList)      # Creates a NEW iterator object

I.__next__()   # 1
I.__next__()   # 2
I.__next__()   # 3
I.__next__()   # 4
I.__next__()   # StopIteration
```

```python
# Key difference: list ≠ its own iterator
iter(myList) is myList   # False ← list creates a separate iterator

# But a file IS its own iterator
f = open("hello.py")
iter(f) is f             # True
iter(f) is f.__iter__()  # True
```

| Object | `iter(obj) is obj` | Notes |
|--------|-------------------|-------|
| File | ✅ `True` | File is its own iterator |
| List | ❌ `False` | List creates a new iterator each time |
| Dict | ❌ `False` | Same as list |
| Range | ❌ `False` | Same as list |

---

## 7. Iterating Over Dictionaries

```python
D = {'a': 1, 'b': 2}

# Using for loop on keys
for key in D.keys():
    print(key)   # a, b

# Using iter() manually
I = iter(D)          # dict_keyiterator
next(I)   # 'a'
next(I)   # 'b'
next(I)   # StopIteration
```

- `iter(D)` by default iterates over **keys**.
- `next()` is the clean built-in equivalent of `.__next__()`.

---

## 8. `range()` is Iterable but NOT an Iterator

```python
R = range(5)      # range(0, 5) — just a description, not yet iterated
I = iter(R)       # range_iterator — now it's an iterator

next(I)   # 0
next(I)   # 1
next(I)   # 2
next(I)   # 3
next(I)   # 4
next(I)   # StopIteration
```

- `range(5)` is **lazy** — it doesn't generate all numbers in memory.
- You need `iter()` to get an iterator from it, or just use it in a `for` loop directly.

---

## 9. Common Errors & Fixes

| Error | Cause | Fix |
|-------|-------|-----|
| `FileNotFoundError` | File doesn't exist | Check filename/path |
| `StopIteration` | Called `next()` past the end | Use `for` loop or check before calling |
| `IndentationError` | Empty `if` block | Always add indented body |
| `SyntaxError: expected ':'` | Missing `:` in `for` | `for key in D.keys():` |
| `TypeError: next expected at least 1 argument` | Called `next()` with no args | Pass the iterator: `next(I)` |

---

## 10. Big Picture — The Iterator Protocol

```
Iterable  ──── iter() ────►  Iterator  ──── next() ────►  Values
(list, file,                  (__iter__,                   one at a time
 dict, range)                  __next__)                   until StopIteration
```

- **Iterable**: anything you can loop over (`list`, `str`, `dict`, `file`, `range`).
- **Iterator**: an object that remembers its position and produces the next value on demand.
- A `for` loop calls `iter()` once, then `next()` repeatedly — automatically.

---

## Quick Reference

```python
# File reading
f = open('file.py')
for line in f:
    print(line, end="")

# Manual iterator
I = iter([1, 2, 3])
next(I)   # 1

# While loop with file
while True:
    line = f.readline()
    if not line: break
    print(line, end="")

# Dict iteration
for key in D:        # iterates keys by default
    print(key)

# Range iteration
for i in range(5):   # 0, 1, 2, 3, 4
    print(i)
```

---

*Notes based on Python 3.12 — Happy studying! 📚*