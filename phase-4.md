
## Topics: Sets, Tuples, Dictionaries, Lambda & Hashing


---

## Q1. Common Elements in Two Lists

**Concept:** Sets — Intersection

```python
a = [1, 2, 3, 4, 5, 6]
b = [4, 5, 6, 7, 8, 9]

a = set(a)
b = set(b)

print(a.intersection(b))
```

**Output:**
```python
{4, 5, 6}
```

Shortcut:
```python
print(a & b)
```

---

## Q2. Symmetric Difference

**Concept:** Set Symmetric Difference

Find elements present in either set but not in both.

```python
a = set([1, 2, 3, 4, 5])
b = set([4, 5, 6, 7, 8])

print(a ^ b)
```

**Output:**
```python
{1, 2, 3, 6, 7, 8}
```

Important Set Operations:

| Operation | Meaning |
|---|---|
| `a.intersection(b)` | Common elements |
| `a.union(b)` | All unique elements |
| `a.difference(b)` | Elements in A but not B |
| `a.symmetric_difference(b)` | Elements in either, but not both |
| `a & b` | Intersection |
| `a \| b` | Union |
| `a - b` | Difference |
| `a ^ b` | Symmetric Difference |

---

## Q3. Remove Duplicates Using Set

**Concept:** Set automatically removes duplicate values.

```python
numbers = [4, 2, 4, 5, 2, 7, 8, 5]

print(set(numbers))
```

**Output:**
```python
{2, 4, 5, 7, 8}
```

Important:
- Lists allow duplicate values.
- Sets store only unique elements.
- Sets do not guarantee insertion order.
- Sets are mutable.
- Set elements must be hashable.

---

## Q4. Find Unique Pairs

**Concept:** Nested Loops + Set + Tuples

Find all unique pairs whose sum equals the target.

```python
num = [1, 2, 3, 4, 5, 6]
result = set()
target = 7

for i in range(len(num)):
    for j in range(i + 1, len(num)):
        if target == num[i] + num[j]:
            result.add((num[i], num[j]))

print(result)
```

**Output:**
```python
{(1, 6), (2, 5), (3, 4)}
```

Important concepts:

- `j = i + 1` prevents reversed duplicate pairs.
- `add()` inserts an element into a set.
- Tuples are hashable, so they can be stored inside sets.
- `append()` is used for lists, while `add()` is used for sets.

**Time Complexity:** O(n²)

---

## Q5. Sort List of Tuples

**Concept:** Tuples + sorted() + Lambda

```python
students = [
    ("Aman", 85),
    ("Riya", 92),
    ("Karan", 78),
    ("Neha", 95)
]

result = sorted(students, key=lambda x: x[1])

print(result)
```

**Output:**
```python
[
    ('Karan', 78),
    ('Aman', 85),
    ('Riya', 92),
    ('Neha', 95)
]
```

### sort() vs sorted()

| Feature | sort() | sorted() |
|---|---|---|
| Type | List method | Built-in function |
| Original list | Changes | Unchanged |
| Return | None | New sorted list |
| Works with | Lists | Any iterable |

### Lambda Function

```python
key=lambda x: x[1]
```

- `lambda` creates an anonymous function.
- `x` represents one tuple.
- `x[0]` represents the name.
- `x[1]` represents the marks.
- `key` tells Python which value to use for sorting.

Descending order:

```python
students.sort(key=lambda x: x[1], reverse=True)
```

Another example — sort words by length:

```python
words = ["apple", "hi", "banana", "cat"]

print(sorted(words, key=lambda x: len(x)))
```

---

## Q6. Group Words by First Character

**Concept:** Dictionary + Lists + append()

```python
words = ["apple", "ant", "banana", "ball", "cat", "car"]

result = {}

for i in range(len(words)):
    s = words[i]

    if s[0] in result:
        result[s[0]].append(words[i])
    else:
        result[s[0]] = [words[i]]

print(result)
```

**Output:**
```python
{
    'a': ['apple', 'ant'],
    'b': ['banana', 'ball'],
    'c': ['cat', 'car']
}
```

Important:

```python
result[key].append(value)
```

Correct way to append an element to an existing list.

Do not write:

```python
result[key] = result[key].append(value)
```

Because `append()` returns `None`.

---

## Q7. Merge Two Dictionaries

**Concept:** Dictionary + items() + Tuple Unpacking

```python
d1 = {"a": 10, "b": 20}
d2 = {"c": 30, "d": 40}

d3 = {}

for key, value in d1.items():
    d3[key] = value

for key, value in d2.items():
    d3[key] = value

print(d3)
```

**Output:**
```python
{'a': 10, 'b': 20, 'c': 30, 'd': 40}
```

Important concepts:

- `items()` returns key-value pairs.
- `key, value` performs tuple unpacking.
- `d3[key] = value` inserts a key-value pair.
- If both dictionaries contain the same key, the second dictionary's value overwrites the first.

---

## Q8. Sort Elements by Frequency

**Concept:** Dictionary + Frequency Counting + sorted() + Lambda

Given:

```python
numbers = [4, 2, 4, 5, 2, 7, 8, 5, 4]
```

### Step 1: Count Frequency

```python
freq = {}

for num in numbers:
    if num in freq:
        freq[num] += 1
    else:
        freq[num] = 1

print(freq)
```

Output:

```python
{4: 3, 2: 2, 5: 2, 7: 1, 8: 1}
```

### Step 2: Sort by Frequency

```python
sorted_items = sorted(
    freq.items(),
    key=lambda x: x[1],
    reverse=True
)
```

Here:
- `freq.items()` returns key-value pairs.
- `x[0]` represents the number.
- `x[1]` represents its frequency.
- `reverse=True` sorts in descending order.

### Step 3: Build Final List

```python
result = []

for key, value in sorted_items:
    for i in range(value):
        result.append(key)

print(result)
```

**Output:**

```python
[4, 4, 4, 2, 2, 5, 5, 7, 8]
```

Complete solution:

```python
numbers = [4, 2, 4, 5, 2, 7, 8, 5, 4]

freq = {}

for num in numbers:
    if num in freq:
        freq[num] += 1
    else:
        freq[num] = 1

sorted_items = sorted(
    freq.items(),
    key=lambda x: x[1],
    reverse=True
)

result = []

for key, value in sorted_items:
    for i in range(value):
        result.append(key)

print(result)
```

**Complexity:** O(n + k log k), where k is the number of distinct elements.

---

## Q9. Two Sum — Optimized Using Dictionary

**Concept:** Hashing + Dictionary + Single Pass

Given:

```python
numbers = [2, 7, 11, 15]
target = 9
```

Expected output:

```python
(0, 1)
```

### Solution

```python
numbers = [2, 7, 11, 15]
target = 9

seen = {}

for i in range(len(numbers)):
    required = target - numbers[i]

    if required in seen:
        print((seen[required], i))
        break

    seen[numbers[i]] = i
```

**Output:**

```python
(0, 1)
```

### Explanation

1. Current number = 2.
2. Required number = 9 - 2 = 7.
3. 7 is not in dictionary, so store `{2: 0}`.
4. Current number = 7.
5. Required number = 9 - 7 = 2.
6. 2 already exists in dictionary at index 0.
7. Answer = `(0, 1)`.

**Complexity:**
- Time: O(n) average.
- Space: O(n).

This is faster than the nested-loop approach, which takes O(n²).

---

## Q10. Group Anagrams

**Concept:** Dictionary + Hashing + Sorting

Anagrams are words containing the same characters in a different order.

Example:
- eat
- tea
- ate

All three are anagrams.

Given:

```python
words = ["eat", "tea", "tan", "ate", "nat", "bat"]
```

Expected output:

```python
[
    ['eat', 'tea', 'ate'],
    ['tan', 'nat'],
    ['bat']
]
```

### Solution

```python
words = ["eat", "tea", "tan", "ate", "nat", "bat"]

groups = {}

for word in words:
    key = "".join(sorted(word))

    if key in groups:
        groups[key].append(word)
    else:
        groups[key] = [word]

print(list(groups.values()))
```

**Output:**

```python
[
    ['eat', 'tea', 'ate'],
    ['tan', 'nat'],
    ['bat']
]
```

### Explanation

For every word, sort its characters:

| Word | Sorted key |
|---|---|
| eat | aet |
| tea | aet |
| tan | ant |
| ate | aet |
| nat | ant |
| bat | abt |

Words having the same sorted key are grouped together.

Important:
- `sorted(word)` returns a sorted list of characters.
- `"".join()` combines those characters into a string.
- Dictionary keys group words with the same signature.
- `groups.values()` returns all grouped lists.

**Complexity:** O(n × m log m), where n is the number of words and m is the maximum word length.

---



Today's most important patterns:

1. **Set:** Use when unique elements or fast membership checks are needed.
2. **Dictionary:** Use for frequency counting, grouping and lookup.
3. **Tuple:** Useful for immutable pairs and dictionary/set keys.
4. **Lambda:** Useful for custom sorting.
5. **Hashing:** Helps optimize problems from O(n²) to O(n) in suitable cases.

