

## Topics Covered

- Python Dictionaries
- Key-Value Pairs
- Dictionary iteration
- `keys()`, `values()`, `items()`
- Frequency counting
- Finding repeated and non-repeated elements
- Maximum frequency
- Character and word frequency
- Conditional filtering

---

## Q1. Count Frequency of Numbers

**Problem:** Count how many times each number appears.

```python
numbers = [1, 2, 2, 3, 1, 4, 2, 3, 5]

count = {}

for i in range(0, len(numbers)):
    if numbers[i] in count:
        count[numbers[i]] = count[numbers[i]] + 1
    else:
        count[numbers[i]] = 1

print(count)
```

**Output:**
```text
{1: 2, 2: 3, 3: 2, 4: 1, 5: 1}
```

## Q2. Find the Most Frequent Number

```python
numbers = [4, 5, 4, 2, 5, 4, 3, 2]

count = {}
Most_frequent_number = 0
Frequency = 0

for i in range(0, len(numbers)):
    if numbers[i] in count:
        count[numbers[i]] = count[numbers[i]] + 1
    else:
        count[numbers[i]] = 1

    if Frequency < count[numbers[i]]:
        Frequency = count[numbers[i]]
        Most_frequent_number = numbers[i]

print("Most_frequent_number:", Most_frequent_number)
print("Frequency:", Frequency)
```

**Output:**
```text
Most_frequent_number: 4
Frequency: 3
```

## Q3. Find the First Repeated Number

```python
numbers = [10, 20, 30, 40, 20, 50, 10]

count = {}

for i in range(0, len(numbers)):
    if numbers[i] in count:
        count[numbers[i]] = count[numbers[i]] + 1
    else:
        count[numbers[i]] = 1

    if count[numbers[i]] > 1:
        print("First repeated number:", numbers[i])
        break
```

**Output:**
```text
First repeated number: 20
```

## Q4. Count Frequency of Words

```python
words = ["apple", "banana", "apple", "mango", "banana", "apple"]

count = {}

for i in range(0, len(words)):
    if words[i] in count:
        count[words[i]] = count[words[i]] + 1
    else:
        count[words[i]] = 1

print(count)
```

**Output:**
```text
{'apple': 3, 'banana': 2, 'mango': 1}
```

## Q5. Find the First Non-Repeating Number

```python
numbers = [4, 5, 1, 2, 1, 4, 5, 6]

count = {}

for i in range(0, len(numbers)):
    if numbers[i] in count:
        count[numbers[i]] = count[numbers[i]] + 1
    else:
        count[numbers[i]] = 1

for key, value in count.items():
    if value == 1:
        print(key)
        break
```

**Output:**
```text
2
```

## Q6. Find Numbers Having Frequency Exactly 2

```python
numbers = [1, 2, 3, 2, 4, 5, 1, 6, 3, 3]

count = {}

for i in range(0, len(numbers)):
    if numbers[i] in count:
        count[numbers[i]] = count[numbers[i]] + 1
    else:
        count[numbers[i]] = 1

for key, value in count.items():
    if value == 2:
        print(key)
```

**Output:**
```text
1
2
```

## Q7. Find the Most Frequent Word

```python
words = ["java", "python", "java", "cpp", "python", "java", "sql"]

count = {}

for i in range(0, len(words)):
    if words[i] in count:
        count[words[i]] = count[words[i]] + 1
    else:
        count[words[i]] = 1

Frequency = 0
Most_frequent_word = ""

for key, value in count.items():
    if value > Frequency:
        Frequency = value
        Most_frequent_word = key

print("Most frequent word:", Most_frequent_word)
print("Frequency:", Frequency)
```

**Output:**
```text
Most frequent word: java
Frequency: 3
```

## Q8. Count Vowels Using a Dictionary

```python
s = "programming"

count = {}

for i in range(0, len(s)):
    if s[i] == 'a' or s[i] == 'e' or s[i] == 'i' or s[i] == 'o' or s[i] == 'u':
        if s[i] in count:
            count[s[i]] = count[s[i]] + 1
        else:
            count[s[i]] = 1

print(count)
```

**Output:**
```text
{'o': 1, 'a': 1, 'i': 1}
```

## Q9. Count Character Frequency (Ignore Spaces)

```python
s = "Hello World"

count = {}

for i in range(0, len(s)):
    if s[i] != " ":
        if s[i] in count:
            count[s[i]] = count[s[i]] + 1
        else:
            count[s[i]] = 1

print(count)
```

**Output:**
```text
{'H': 1, 'e': 1, 'l': 3, 'o': 2, 'W': 1, 'r': 1, 'd': 1}
```

## Q10. Find Duplicate Characters

```python
s = "programming"

count = {}

for i in range(0, len(s)):
    if s[i] in count:
        count[s[i]] = count[s[i]] + 1
    else:
        count[s[i]] = 1

for key, value in count.items():
    if value > 1:
        print(key, ":", value)
```

**Output:**
```text
r : 2
g : 2
m : 2
```

---

## Important Dictionary Concepts

### 1. Creating a Dictionary

```python
count = {}
```

### 2. Adding Elements

```python
count["apple"] = 1
```

### 3. Checking Whether a Key Exists

```python
if "apple" in count:
    print("Found")
```

### 4. Updating Values

```python
count["apple"] = count["apple"] + 1
```

### 5. Iterating Through Keys

```python
for key in count:
    print(key)
```

### 6. Iterating Through Values

```python
for value in count.values():
    print(value)
```

### 7. Iterating Through Keys and Values

```python
for key, value in count.items():
    print(key, value)
```

---

## Key Learnings

1. Dictionaries store data in key-value pairs.
2. Dictionary keys can be checked using `in`.
3. Frequency counting is a common dictionary application.
4. `.items()` allows access to both keys and values.
5. `break` stops a loop when the required condition is satisfied.
6. A second loop can be used to filter or find maximum/minimum frequencies.
7. Dictionaries are useful for counting numbers, words and characters.

