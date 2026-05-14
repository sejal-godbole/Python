# Python Dictionaries — Study Notes 🐍
> Based on hands-on REPL practice | Python 3.12

---

## 1. Dictionary Basics

A **dictionary** stores data as **key-value pairs**. Keys must be unique.

```python
chai_types = {"Masala": "Spicy", "Ginger": "Zesty", "Green": "Mild"}
```

- Keys → `"Masala"`, `"Ginger"`, `"Green"`
- Values → `"Spicy"`, `"Zesty"`, `"Mild"`

---

## 2. Accessing Values

### `[]` — direct access
```python
chai_types["Masala"]     # 'Spicy'
chai_types["Masalaa"]    # ❌ KeyError — key doesn't exist
```

### `.get()` — safe access
```python
chai_types.get("Ginger")    # 'Zesty'
chai_types.get("Gingery")   # None  ← no error, just returns None
chai_types.get("Gingery", "Not found")  # 'Not found'  ← custom default
```

> **Rule:** Prefer `.get()` when a key might not exist — avoids crashing your program.

---

## 3. Adding & Updating

```python
chai_types["Green"] = "Fresh"      # update existing key
chai_types["Earl Grey"] = "Citrus" # add new key
```

Same syntax for both — Python creates the key if it doesn't exist, updates if it does.

---

## 4. Looping Over a Dictionary

### Keys only (default)
```python
for chai in chai_types:
    print(chai)
# Masala
# Ginger
# Green
```

### Keys + values manually
```python
for chai in chai_types:
    print(chai, chai_types[chai])
```

### Keys + values with `.items()` ✓ (preferred)
```python
for key, value in chai_types.items():
    print(key, value)
# Masala Spicy
# Ginger Zesty
# Green Fresh
```

> ⚠️ **Typo from your session:** `values` (plural) in the unpacking but `value` (singular) in the print caused a `NameError`. Variable names in `for key, value` must match exactly what you use in the loop body.

---

## 5. Membership Check & Length

```python
if "Masala" in chai_types:
    print("I have masala chai")   # checks keys only

len(chai_types)    # 3
```

---

## 6. Removing Items

### `pop(key)` — remove by key, returns value
```python
chai_types.pop("Ginger")    # returns 'Zesty', removes 'Ginger'
```

### `popitem()` — remove & return last inserted pair
```python
chai_types.popitem()    # returns ('Earl Grey', 'Citrus')
```

### `del` — delete by key
```python
del chai_types["Green"]
```

### `clear()` — empty the entire dictionary
```python
chai_types.clear()
chai_types    # {}
```

| Method | Returns | Use when |
|---|---|---|
| `pop(key)` | The value | You need the removed value |
| `popitem()` | `(key, value)` tuple | Remove last item |
| `del d[key]` | Nothing | Just delete, no return needed |
| `clear()` | Nothing | Wipe everything |

---

## 7. Copying a Dictionary

```python
chai_types_copy = chai_types.copy()   # independent shallow copy
```

Same rule as lists — `copy_dict = original` is a reference, not a copy!

---

## 8. Nested Dictionaries

Dictionaries can contain other dictionaries as values:

```python
tea_shop = {
    "chai": {"Masala": "Spicy", "Ginger": "Zesty"},
    "Tea":  {"Green": "Mild",   "Black": "Strong"}
}

tea_shop["chai"]            # {'Masala': 'Spicy', 'Ginger': 'Zesty'}
tea_shop["chai"]["Ginger"]  # 'Zesty'
```

Access nested values by chaining `[]` operators.

---

## 9. Dictionary Comprehension

Build a dictionary in one line — same idea as list comprehension:

```python
squared_num = {x: x ** 2 for x in range(6)}
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```

**Syntax:**
```
{key_expr : value_expr  for  item  in  iterable}
```

---

## 10. `dict.fromkeys()` — Build Dict from a List

Creates a new dictionary from a list of keys, all set to the same default value.

```python
keys = ["Masala", "Ginger", "Lemon"]

dict.fromkeys(keys, "Delicious")
# {'Masala': 'Delicious', 'Ginger': 'Delicious', 'Lemon': 'Delicious'}
```

### ⚠️ Gotcha — shared mutable default

```python
dict.fromkeys(keys, keys)
# {'Masala': ['Masala', 'Ginger', 'Lemon'],
#  'Ginger': ['Masala', 'Ginger', 'Lemon'],
#  'Lemon':  ['Masala', 'Ginger', 'Lemon']}
```

All three keys point to the **same list object**. Modifying one value modifies all of them! Use with caution when the default is mutable (list, dict, etc.).

---

## 🧠 Quick Recap Table

| Topic | Key Takeaway |
|---|---|
| `d[key]` | Raises `KeyError` if missing |
| `d.get(key)` | Returns `None` if missing — safe |
| `d[key] = val` | Add or update |
| `in` operator | Checks **keys** only |
| `.items()` | Returns `(key, value)` pairs for looping |
| `pop(key)` | Remove by key, returns value |
| `popitem()` | Remove last inserted pair |
| `clear()` | Empties the whole dict |
| `.copy()` | Independent copy — not `b = a` |
| `{k: v for ...}` | Dictionary comprehension |
| `dict.fromkeys(list, val)` | Build dict from list of keys |

---

*Dictionaries: Python's most powerful data structure! ☕🚀*