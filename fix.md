2025-06-01

## 1. modify `is not` to `!=` in line 95

I mean line 95:
```python
    for c in line:
        if c != ' ' and c != '  ':
            return c == ' '
    return line
```

not line 666 `is None`

### 1.1 Why use `!=` here?

- `!=` checks if the value of `c` is not equal to `' '` (a single space) or `'  '` (two spaces).
- `is not` checks if `c` is not the same object as `' '` or `'  '`.

You should use `!=` for string value comparison.  
Using `is not` for strings can give unexpected results, because two different string objects with the same value are not guaranteed to be the same object in memory.

------

### 1.2

Why not modify
```python
if not self.maybe_automatic_link is None:
```
to
```python
if self.maybe_automatic_link != None:
```

Explanation:
- Both forms check if `self.maybe_automatic_link` is not `None`.
- `is not` checks for **object identity** (whether it is exactly the `None` object).
- `!=` checks for **value inequality comparison** (whether the value is not equal to `None`).
- In most cases for `None`, both work similarly, but `is not None` is the preferred and more Pythonic way to check for `None`.
- Changing to `!= None` is less strict and can be affected if the class defines a custom `__eq__` method.

## 2. modify `data = re.sub('\s+', ' ', data)` to `data = re.sub(r'\s+', ' ', data)` in line 589

```python
data = re.sub('\s+', ' ', data)
```
should be changed to:
```python
data = re.sub(r'\s+', ' ', data)
```

- `re.sub(pattern, repl, string)` replaces all occurrences of the regex `pattern` in `string` with `repl`.
- `\s+` is a regex pattern that matches one or more whitespace characters.
- **In Python, writing `'\s+'` without the `r` (raw string) can cause issues because `\s` is interpreted as an escape sequence by Python, not by the regex engine.**
- Using `r'\s+'` (a raw string) ensures that `\s` is passed correctly to the regex engine as a whitespace matcher.

2025-07-17

## 3. use `range` instead `xrange` in line 607
