# 🐍 Python Tuples — Study Notes

> **Tuples** are ordered, immutable sequences in Python. Think of them as *read-only lists*.

---

## 1. Defining a Tuple & Finding Its Length

```python
tea_types = ("Black", "Green", "Oolong")
tea_types        # ('Black', 'Green', 'Oolong')
len(tea_types)   # 3
```

- Use **parentheses `()`** to define a tuple.
- `len()` returns the number of elements.

---

## 2. Indexing & Slicing

```python
tea_types[0]    # 'Black'      → first element
tea_types[-1]   # 'Oolong'     → last element (negative index)
tea_types[1:]   # ('Green', 'Oolong')   → from index 1 onwards
tea_types[:2]   # ('Black', 'Green')    → up to (not including) index 2
```

| Operation | Syntax | Result |
|-----------|--------|--------|
| First item | `tuple[0]` | `'Black'` |
| Last item | `tuple[-1]` | `'Oolong'` |
| Slice from index | `tuple[1:]` | `('Green', 'Oolong')` |
| Slice up to index | `tuple[:2]` | `('Black', 'Green')` |

> 💡 Slicing works the same way as with lists and strings.

---

## 3. Immutability — The Key Property of Tuples

```python
tea_types[0] = "Lemon"
# ❌ TypeError: 'tuple' object does not support item assignment
```

- **You cannot change, add, or remove elements** once a tuple is created.
- This is what makes tuples different from lists.
- Use tuples when data should **not be modified** (e.g., coordinates, config values).

---

## 4. Concatenation & Repetition

```python
more_tea = ("Herbal", "Earl Grey")

# Concatenation (+)
all_tea = tea_types + more_tea
all_tea  # ('Black', 'Green', 'Oolong', 'Herbal', 'Earl Grey')

# Membership test (in)
if "Green" in all_tea:
    print("I have green tea")   # Output: I have green tea

# Repetition (*)
nested_tea = more_tea * 2
nested_tea  # ('Herbal', 'Earl Grey', 'Herbal', 'Earl Grey')
```

> ⚠️ `+` and `*` don't modify the original tuple — they create **new** tuples.

---

## 5. Tuple Methods

Tuples have only **two built-in methods**:

```python
nested_tea.count("Herbal")      # 2  → counts occurrences
nested_tea.index("Earl Grey")   # 1  → returns index of first match
```

| Method | Purpose | Example |
|--------|---------|---------|
| `.count(x)` | Count how many times `x` appears | `nested_tea.count("Herbal")` → `2` |
| `.index(x)` | Find the index of the first `x` | `nested_tea.index("Earl Grey")` → `1` |

---

## 6. Internal Mutability (Tricky! ⚠️)

```python
tuple_with_list = ("Black", "Green", ["Ginger", "Lemon"])
tuple_with_list[2].append("Honey")
tuple_with_list
# ('Black', 'Green', ['Ginger', 'Lemon', 'Honey'])
```

- The **tuple itself** is immutable — you can't replace `tuple_with_list[2]`.
- But if a tuple **contains a mutable object** (like a list), that object *can* be changed internally.
- The tuple still holds a reference to the same list; the list just grew.

> 🧠 Remember: Immutability means the tuple's *references* are fixed, not necessarily the objects those references point to.

---

## Quick Summary

| Feature | Tuple |
|---------|-------|
| Syntax | `(item1, item2)` |
| Ordered | ✅ Yes |
| Mutable | ❌ No |
| Allows duplicates | ✅ Yes |
| Methods available | `count()`, `index()` |
| Supports indexing/slicing | ✅ Yes |
| Can hold mixed types | ✅ Yes |

---

## When to Use Tuples vs Lists

| Use a **Tuple** when... | Use a **List** when... |
|------------------------|----------------------|
| Data shouldn't change | Data needs to be modified |
| Returning multiple values from a function | Storing a growing collection |
| Using as dictionary keys | Order matters but items change |
| Slightly faster & memory efficient | You need `.append()`, `.remove()`, etc. |

---

*Notes based on Python 3.x — Happy studying! 📚*