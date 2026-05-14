# Python Strings — Study Notes 🐍
> Based on hands-on REPL practice | Python 3.12

---

## 1. String Basics

```python
chai = "Lemon chai"
chai          # 'Lemon chai'  → REPL shows with quotes
print(chai)   # Lemon chai   → print shows without quotes
```

Strings are **immutable** — operations return a new string; the original never changes.

```python
chai = "Masala chai"
chai.replace("Masala", "Ginger")   # 'Ginger chai'
chai                                # 'Masala chai'  ← unchanged!
```

---

## 2. Indexing

Access individual characters using `[]`. Index starts at **0**.

```python
chai = "Masala chai"
chai[0]    # 'M'   → first character
chai[-1]   # 'i'   → last character (negative index counts from end)
```

| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Char | M | a | s | a | l | a |   | c | h | a | i |

---

## 3. Slicing

Syntax: `string[start : stop : step]`

```python
num_list = "0123456789"

num_list[:]       # '0123456789'  → full string
num_list[3:]      # '3456789'     → from index 3 to end
num_list[:7]      # '0123456'     → from start up to (not including) index 7
num_list[0:7:2]   # '0246'        → every 2nd character from 0 to 7
num_list[0:7:3]   # '036'         → every 3rd character from 0 to 7
```

> **Rule:** `stop` index is **exclusive** — `[:7]` gives indices 0–6, not 0–7.

---

## 4. Common String Methods

### Case
```python
chai = "Masala chai"
chai.lower()   # 'masala chai'
chai.upper()   # 'MASALA CHAI'
```

### Strip whitespace
```python
chai = "    masala chai   "
chai.strip()   # 'masala chai'  → removes leading & trailing spaces
```

### Replace
```python
chai = "Lemon chai"
chai.replace("Lemon", "Ginger")   # 'Ginger chai'
```

### Split
```python
chai = "Lemon, Ginger, Masala, Mint"
chai.split(", ")   # ['Lemon', 'Ginger', 'Masala', 'Mint']
```
Splits the string into a **list** using the given separator.

### Find
```python
chai = "Masala Chai"
chai.find("Chai")    #  7   → returns starting index
chai.find("chai")    # -1   → returns -1 if NOT found (case-sensitive!)
```

### Count
```python
chai = "Masala Chai Chai Chai"
chai.count("Chai")    # 3
chai.count("chai")    # 0   → case-sensitive!
```

### Length
```python
chai = "Masala Chai"
len(chai)    # 11   → counts spaces too
```

---

## 5. String Formatting

### `.format()` method
```python
order = "I ordered {} cups of {} chai"
order.format(2, "Masala")   # 'I ordered 2 cups of Masala chai'
```

Placeholders `{}` are filled **left to right** by the arguments.

### f-strings (modern, preferred)
```python
quantity = 2
chai_type = "Masala"
f"I ordered {quantity} cups of {chai_type} chai"
# 'I ordered 2 cups of Masala chai'
```

---

## 6. Join

The opposite of `split()` — joins a list of strings into one.

```python
chai_variety = ["Lemon", "Masala", "Ginger"]

"".join(chai_variety)    # 'LemonMasalaGinger'
" ".join(chai_variety)   # 'Lemon Masala Ginger'
", ".join(chai_variety)  # 'Lemon, Masala, Ginger'
```

> **Syntax tip:** The separator goes on the **left** of `.join()`, the list goes inside.

---

## 7. Iterating Over a String

Strings are iterable — you can loop over each character:

```python
chai = "Masala Chai"
for letter in chai:
    print(letter)
# M
# a
# s
# a
# l
# a
#   (space)
# C
# h
# a
# i
```

---

## 8. The `in` Operator

```python
"Masala" in "Masala Chai"   # True
"Masala" in "c:\\user\\pwd" # False
```

Checks if a substring exists inside a string. Case-sensitive.

---

## 9. Escape Characters & Raw Strings

### Escape characters
```python
chai = "He said, \"Masala chai is awesome\"."
# He said, "Masala chai is awesome".

chai = "Masala\nChai"
print(chai)
# Masala
# Chai
```

| Escape | Meaning |
|---|---|
| `\"` | Double quote inside a string |
| `\'` | Single quote inside a string |
| `\n` | Newline |
| `\t` | Tab |
| `\\` | Literal backslash |

### Raw strings — `r"..."`

Prefix `r` tells Python to **ignore escape sequences**. Useful for file paths and regex.

```python
chai = r"Masala\nChai"
print(chai)    # Masala\nChai  ← \n is NOT treated as newline

chai = r"c:\user\pwd"
print(chai)    # c:\user\pwd  ← backslashes are literal
```

### ⚠️ Raw string gotcha

A raw string **cannot end with an odd number of backslashes**:

```python
r"c:\user\pwd\"    # SyntaxError! ← backslash at end escapes the closing quote
r"c:\user\pwd\\"   # OK → ends with \\, which is two backslashes
```

---

## 🧠 Quick Recap Table

| Topic | Key Takeaway |
|---|---|
| Strings are immutable | Methods return new strings; original unchanged |
| Indexing | Starts at 0; `-1` is last character |
| Slicing `[start:stop:step]` | `stop` is exclusive |
| `.find()` | Returns index or `-1` if not found |
| `.split()` | String → List |
| `"sep".join(list)` | List → String |
| Case sensitivity | `.find()`, `.count()`, `in` are all case-sensitive |
| `r"..."` | Raw string — backslashes are literal |
| Raw string can't end with `\` | Use `\\` at the end instead |

---

*Keep sipping chai and coding! ☕🚀*