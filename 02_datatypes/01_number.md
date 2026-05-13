# Python Basics — Study Notes 🐍
> Based on hands-on REPL practice | Python 3.12

---

## 1. Variables & Basic Arithmetic

Variables are assigned with `=`. Python supports all standard arithmetic operators.

```python
x = 2
y = 3
z = 4

x + y        # 5
x + y * 2    # 8  → multiplication has higher precedence than addition
40 + 2.23    # 42.23 → int + float = float
```

> **Key Concept:** Python follows standard **BODMAS/PEMDAS** operator precedence.

---

## 2. Type Conversion

```python
int(2.23)     # 2  → truncates the decimal part (does NOT round)
int(3.14)     # 3
```

---

## 3. String Concatenation

```python
"sejal" + "sampat" + "godbole"   # 'sejalsampatgodbole'
```

Strings are joined with `+`. No space is added automatically — you must add it manually if needed.

---

## 4. Multiple Values & Expressions

```python
x, y, z        # (2, 3, 4)   → displays as a tuple
x + 1, y * 2   # (3, 6)      → multiple expressions return a tuple
```

---

## 5. Power Operator & Big Integers

```python
2 ** 1000     # a huge number!
```

Python supports **arbitrarily large integers** — no overflow like in C/Java.

```python
999999999999999999999999999999999999999999 + 1   # works perfectly
999999999999999999999999999999999999999999 * 2.1  # returns a float (loses precision)
```

> **Note:** Mixing huge integers with floats causes precision loss. Use `Decimal` for precision.

---

## 6. Comparison Operators

```python
1 < 2       # True
5.0 == 5.0  # True
4.0 != 5.0  # True
```

Returns `True` or `False` (Boolean values).

---

## 7. The `math` Module

```python
import math

math.floor(-3.5)   # -4  → rounds DOWN (toward negative infinity)
math.floor(3.9)    #  3

math.trunc(2.8)    #  2  → removes decimal, moves toward ZERO
math.trunc(-2.8)   # -2
```

| Function | Behavior |
|---|---|
| `math.floor(x)` | Rounds toward −∞ |
| `math.ceil(x)` | Rounds toward +∞ |
| `math.trunc(x)` | Truncates toward 0 |

---

## 8. Complex Numbers

```python
2 + 1j          # (2+1j)
2 + 1j * 3      # (2+3j)   → operator precedence: 1j*3 first
(2 + 1j) * 3    # (6+3j)   → multiply whole complex number
```

`j` is the imaginary unit in Python (mathematics uses `i`).

---

## 9. Number Systems (Literals & Conversions)

### Literals
```python
0o20    # 16   → Octal  (prefix: 0o)
0xFF    # 255  → Hexadecimal (prefix: 0x)
0b1000  # 8    → Binary (prefix: 0b)
```

### Converting to other bases
```python
oct(64)   # '0o100'
hex(64)   # '0x40'
bin(64)   # '0b1000000'
```

### Parsing strings as different bases
```python
int('64', 8)      # 52   → treat '64' as octal
int('64', 16)     # 100  → treat '64' as hexadecimal
int('10000', 2)   # 16   → treat '10000' as binary
```

---

## 10. Bitwise Shift Operator

```python
x = 1
x << 2    # 4   → left shift: multiply by 2² = 4
```

Left shift `<<` by `n` = multiply by `2ⁿ`
Right shift `>>` by `n` = divide by `2ⁿ`

---

## 11. The `random` Module

```python
import random

random.random()          # float between 0.0 and 1.0
random.randint(1, 10)    # random integer from 1 to 10 (inclusive)

l1 = ['lemon', 'masala', 'ginger', 'mint']
random.choice(l1)        # picks one random element
random.shuffle(l1)       # shuffles the list IN-PLACE (modifies original)
```

> **Important:** `shuffle()` modifies the list directly and returns `None`.

---

## 12. `repr()` vs `str()` vs `print()`

```python
repr('chai')   # "'chai'"  → developer-friendly, includes quotes
str('chai')    # 'chai'    → user-friendly string
print('chai')  # chai      → outputs to console, no quotes
```

| Function | Use Case |
|---|---|
| `repr()` | Debugging; shows exact type representation |
| `str()` | Display to users |
| `print()` | Output to console |

---

## 13. The `decimal` Module — Precise Arithmetic

Floating-point numbers have precision issues:
```python
0.1 + 0.1 + 0.1    # 0.30000000000000004  ← NOT exactly 0.3!
```

Use `Decimal` for financial/scientific calculations:
```python
from decimal import Decimal

Decimal('0.1') + Decimal('0.1') + Decimal('0.1')            # Decimal('0.3') ✓
Decimal('0.1') + Decimal('0.1') + Decimal('0.1') - Decimal('0.3')  # Decimal('0.0') ✓

# ⚠️ Always pass strings to Decimal, not floats!
Decimal(0.3)    # imprecise — float imprecision is already baked in
Decimal('0.3')  # precise ✓
```

---

## 14. The `fractions` Module

```python
from fractions import Fraction

myFra = Fraction(2, 7)   # represents 2/7 exactly
myFra                     # Fraction(2, 7)
```

Useful when you need **exact rational arithmetic** (e.g., 2/7 + 1/3 without floating-point errors).

---

## 🧠 Quick Recap Table

| Topic | Key Takeaway |
|---|---|
| Integers | Unlimited size in Python |
| Floats | Imprecise due to binary representation |
| `Decimal` | Use for exact decimal arithmetic (pass strings!) |
| `Fraction` | Exact rational numbers |
| `math.floor` | Rounds toward −∞ |
| `math.trunc` | Truncates toward 0 |
| `repr()` | For debugging |
| `random.shuffle()` | Modifies list in-place |
| `0b`, `0o`, `0x` | Binary, Octal, Hex literals |

---

*Happy coding! 🚀*