# Python Lists — Study Notes 🐍
> Based on hands-on REPL practice | Python 3.12

---

## 1. List Basics

A **list** is an ordered, mutable (changeable) collection of items.

```python
tea_varieties = ["Black", "Green", "Oolong", "White"]
```

---

## 2. Indexing & Slicing

Same rules as strings:

```python
tea_varieties[0]    # 'Black'   → first element
tea_varieties[-1]   # 'White'   → last element
tea_varieties[1:3]  # ['Green', 'Oolong']  → stop is exclusive
tea_varieties[:2]   # ['Black', 'Green']
tea_varieties[2:]   # ['Oolong', 'White']
```

---

## 3. Modifying Lists

### Single element assignment
```python
tea_varieties[3] = "Herbal"
# ['Black', 'Green', 'Oolong', 'Herbal']
```

### ⚠️ Slice assignment — a common gotcha!

Assigning a **string** to a slice unpacks it character by character:
```python
tea_varieties[1:2] = "Lemon"
# ['Black', 'L', 'e', 'm', 'o', 'n', 'Oolong', 'Herbal']  ← NOT what you want!
```

Always wrap the replacement in a **list**:
```python
tea_varieties[1:2] = ["Lemon"]
# ['Black', 'Lemon', 'Oolong', 'White']  ✓
```

### Replacing multiple elements
```python
tea_varieties[1:3] = ["Green", "Masala"]
# ['Black', 'Green', 'Masala', 'White']
```

### Inserting without replacing — use `[n:n]`
```python
tea_varieties[1:1] = ["test", "test"]
# ['Black', 'test', 'test', 'Green', 'Masala', 'White']
# Nothing was removed — items were inserted at index 1
```

### Deleting elements via slice
```python
tea_varieties[1:3] = []
# ['Black', 'Green', 'Masala', 'White']  ← 'test', 'test' removed
```

---

## 4. Looping Over a List

```python
for tea in tea_varieties:
    print(tea)
# Black
# Green
# Masala
# White

# Custom separator using end=
for tea in tea_varieties:
    print(tea, end="-")
# Black-Green-Masala-White-
```

> **Note:** `end="-"` replaces the default newline `\n` with `-`. The separator also appears after the last item.

---

## 5. Checking Membership

```python
if "Oolong" in tea_varieties:
    print("I have Oolong tea")
```

Returns `True` if the item exists in the list, `False` otherwise.

---

## 6. Common List Methods

### `append()` — add to end
```python
tea_varieties.append("Oolong")
# ['Black', 'Green', 'Masala', 'White', 'Oolong']
```

### `pop()` — remove from end
```python
tea_varieties.pop()     # returns 'Oolong' and removes it
# ['Black', 'Green', 'Masala', 'White']
```
You can also pop by index: `tea_varieties.pop(1)` removes index 1.

### `remove()` — remove by value
```python
tea_varieties.remove("Green")
# ['Black', 'Masala', 'White']
```
Removes the **first occurrence** of the value. Raises `ValueError` if not found.

### `insert()` — add at specific index
```python
tea_varieties.insert(1, "Green")
# ['Black', 'Green', 'Masala', 'White']
```

---

## 7. Copying a List — A Critical Concept!

### ❌ Wrong way (reference copy)
```python
tea_varieties_copy = tea_varieties
```
This does **not** create a new list — both variables point to the **same list** in memory. Changing one changes the other.

### ✓ Right way (shallow copy)
```python
tea_varieties_copy = tea_varieties.copy()
```
Now they are **independent**:
```python
tea_varieties_copy.append("Lemon")
tea_varieties_copy   # ['Black', 'Green', 'Masala', 'White', 'Lemon']
tea_varieties        # ['Black', 'Green', 'Masala', 'White']  ← unchanged ✓
```

Other ways to copy: `list(tea_varieties)` or `tea_varieties[:]`

---

## 8. List Comprehension

A concise way to build lists in one line.

```python
squared_nums = [x ** 2 for x in range(10)]
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

**Syntax:**
```
[expression  for  item  in  iterable]
```

You can also add a condition:
```python
even_squares = [x ** 2 for x in range(10) if x % 2 == 0]
# [0, 4, 16, 36, 64]
```

> List comprehensions are faster and more Pythonic than equivalent `for` loops with `.append()`.

---

## 🧠 Quick Recap Table

| Topic | Key Takeaway |
|---|---|
| `list[n]` | Index access; `-1` is last element |
| `list[1:3]` | Slice; stop index is exclusive |
| `list[1:2] = "str"` | ⚠️ Unpacks string into chars — use `["str"]` instead |
| `list[n:n] = [...]` | Insert without deleting |
| `list[n:m] = []` | Delete a slice |
| `append()` | Add to end |
| `pop()` | Remove & return last (or by index) |
| `remove(val)` | Remove first occurrence by value |
| `insert(i, val)` | Insert at index `i` |
| `copy()` | True independent copy — NOT `b = a` |
| `[expr for x in iter]` | List comprehension |

---

*One list method at a time! ☕🚀*