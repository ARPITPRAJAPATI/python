
## 1. Topics Covered

- Python syntax and indentation
- Variables and data types
- Taking input using `input()`
- Type conversion using `int()` and `float()`
- Arithmetic and comparison operators
- Conditional statements (`if`, `elif`, `else`)
- `for` and `while` loops
- `range()` function
- `break` and `continue`
- String indexing and slicing
- Lists and list traversal
- Dictionaries and key-value pairs
- Functions and `return`
- Recursion and base cases
- Basic sorting concepts

## 2. Problems Practiced

### Q1. Reverse a String

**Concepts:** String indexing, loops, `range()`

```python
s = "hello"
sr = ""

for i in range(len(s)-1, -1, -1):
    sr += s[i]

print(sr)
```

Output: `olleh`

### Q2. Prime Number

**Concepts:** Loops, conditions, modulus operator, break

Learned how to check whether a number has any divisor other than 1 and itself.

### Q3. Factorial of a Number

**Concepts:** Functions, recursion, base case, return

```python
def is_fact(n):
    if n == 0:
        return 1

    return n * is_fact(n-1)

n = int(input())
print(is_fact(n))
```

### Q4. Fibonacci Series

**Concepts:** Loops, variables, updating values

```python
n = int(input())

a = 0
b = 1

for i in range(n):
    print(a, end=" ")
    a, b = b, a + b
```

### Q5. Palindrome String

**Concepts:** String reversal, loops, comparison

Practiced checking whether the original string and reversed string are equal.

Examples:
- `madam` → Palindrome
- `hello` → Not Palindrome

### Q6. Second Largest Element in an Array

**Concepts:** Lists, traversal, conditions, comparison

Practiced finding the second largest distinct element without using sorting or `max()`.

```python
largest = float('-inf')
second_maxy = float('-inf')

for i in range(len(a)):
    if a[i] > largest:
        second_maxy = largest
        largest = a[i]

    elif a[i] > second_maxy and a[i] != largest:
        second_maxy = a[i]
```

### Q7. Sort Dictionary by Value

**Concepts:** Dictionaries, `items()`, `sorted()`, lambda

Learned:
- `data.items()` returns key-value pairs.
- `x[0]` represents the key.
- `x[1]` represents the value.
- `key=lambda x: x[1]` sorts using values.

This topic needs another revision and independent practice.

### Q8. Count Vowels in a String

**Concepts:** Strings, loops, conditions, counters

```python
s = "education"

count = 0

for i in range(0, len(s)):
    if (s[i] == "a" or s[i] == "e" or
        s[i] == "i" or s[i] == "o" or s[i] == "u"):
        count = count + 1

print(count)
```

Output: `5`

### Q9. Common Elements in Two Lists

**Concepts:** Lists, nested loops, comparison

```python
a = [1, 2, 3, 4, 5]
b = [3, 4, 5, 6, 7]

for i in range(0, len(a)):
    for j in range(0, len(b)):
        if a[i] == b[j]:
            print(a[i])
```

Output:
```text
3
4
5
```

### Q10. Leap Year

**Concepts:** If-elif-else, modulus operator, conditions

```python
n = int(input())

if n % 400 == 0:
    print("leap year")

elif n % 100 == 0:
    print("not a leap year")

elif n % 4 == 0:
    print("leap year")

else:
    print("not a leap year")
```

Examples:
- 2024 → Leap Year
- 2023 → Not a Leap Year
- 2000 → Leap Year
- 1900 → Not a Leap Year

---

## 3. Important Python Concepts Learned

| Concept | Understanding |
|---|---|
| `input()` | Takes user input as a string |
| `int()` | Converts input into integer |
| `range()` | Generates a sequence of numbers |
| `len()` | Returns length |
| `break` | Terminates the loop |
| `continue` | Skips current iteration |
| `return` | Sends a value back from a function |
| `print()` | Displays output |
| `[::-1]` | Reverses a sequence |
| `float('-inf')` | Represents negative infinity |
| `items()` | Returns dictionary key-value pairs |
| `lambda` | Creates a small anonymous function |

---

## 4. Key Learnings

1. Python uses indentation instead of curly braces to define code blocks.
2. Strings can be traversed using indexing or directly through a loop.
3. Lists can be traversed using both indices and elements.
4. Nested loops help compare elements of two collections.
5. Recursion requires a proper base case.
6. `return` and `print` have different purposes.
7. Fibonacci can be solved by updating two variables.
8. Dictionary sorting uses key-value pairs.

---



