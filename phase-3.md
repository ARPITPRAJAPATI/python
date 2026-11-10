

## Topics Covered
- List traversal and duplicate removal
- In-place array manipulation
- Mathematical formula
- Dictionary / Hashing
- Two Pointers
- String traversal
- Frequency counting
- Sliding Window
- Kadane's Algorithm

---

## Q1. Remove Duplicates While Preserving Order

**Input:**
```python
numbers = [4, 2, 4, 5, 2, 7, 8, 5]
```

**Output:**
```python
[4, 2, 5, 7, 8]
```

**Solution:**
```python
numbers = [4, 2, 4, 5, 2, 7, 8, 5]
result = []

for i in range(len(numbers)):
    if numbers[i] not in result:
        result.append(numbers[i])

print(result)
```

**Learning:** `append()` adds an element at the end of a list. Avoid removing elements while iterating over the same list because indexes shift.

---

## Q2. Rotate Array by K Positions

**Status:** Pending Revision

**Input:**
```python
numbers = [1, 2, 3, 4, 5]
k = 2
```

**Expected Output:**
```python
[4, 5, 1, 2, 3]
```

---

## Q3. Move Zeroes to the End

**Input:**
```python
numbers = [0, 1, 0, 3, 12]
```

**Output:**
```python
[1, 3, 12, 0, 0]
```

**Solution:**
```python
numbers = [0, 1, 0, 3, 12]
j = 0

for i in range(len(numbers)):
    if numbers[i] != 0 and numbers[i] != numbers[j]:
        temp = numbers[i]
        numbers[i] = numbers[j]
        numbers[j] = temp
        j += 1

print(numbers)
```

**Learning:** Two pointers can be used to move non-zero elements to the beginning while maintaining their order.

---

## Q4. Find the Missing Number

**Input:**
```python
numbers = [1, 2, 3, 5, 6]
```

**Output:**
```python
4
```

**Solution:**
```python
numbers = [1, 2, 3, 5, 6]

n = len(numbers) + 1
total = 0

for i in range(len(numbers)):
    total += numbers[i]

expected_sum = n * (n + 1) // 2
missing = expected_sum - total

print(missing)
```

**Learning:** Sum of first N natural numbers:

`n * (n + 1) // 2`

---

## Q5. Find Pairs With a Given Sum

**Input:**
```python
numbers = [2, 4, 3, 5, 7, 8, 1]
target = 9
```

**Output:**
```python
[(2, 7), (4, 5), (8, 1)]
```

**Solution:**
```python
numbers = [2, 4, 3, 5, 7, 8, 1]
target = 9

seen = {}
result = []

for number in numbers:
    required = target - number

    if required in seen:
        result.append((required, number))
    else:
        seen[number] = True

print(result)
```

**Learning:** Dictionary-based lookup reduces average time complexity from O(n²) to O(n).

---

## Q6. Merge Two Sorted Lists

**Input:**
```python
a = [1, 3, 5, 7]
b = [2, 4, 6, 8]
```

**Output:**
```python
[1, 2, 3, 4, 5, 6, 7, 8]
```

**Solution:**
```python
a = [1, 3, 5, 7]
b = [2, 4, 6, 8]

merge = []
i = 0
j = 0

while i < len(a) and j < len(b):
    if a[i] < b[j]:
        merge.append(a[i])
        i += 1
    else:
        merge.append(b[j])
        j += 1

while i < len(a):
    merge.append(a[i])
    i += 1

while j < len(b):
    merge.append(b[j])
    j += 1

print(merge)
```

**Learning:** Two-pointer technique. Compare current elements and append the smaller one.

**Time Complexity:** O(n + m)

---

## Q7. Find the Longest Word in a Sentence

**Input:**
```python
s = "Python programming is very interesting"
```

**Output:**
```python
programming
```

**Solution:**
```python
s = "Python programming is very interesting"

maxy = ""
count = ""

for i in range(len(s)):
    if s[i] != " ":
        count += s[i]

        if len(count) > len(maxy):
            maxy = count
    else:
        count = ""

print(maxy)
```

**Learning:** Build each word character by character and track the longest word.

---

## Q8. Check Whether Two Strings Are Anagrams

**Input:**
```python
s1 = "listen"
s2 = "silent"
```

**Output:**
```python
Anagram
```

**Solution:**
```python
def anagram(s1, s2):
    freq = {}

    if len(s1) != len(s2):
        return 0

    for i in range(len(s1)):
        if s1[i] in freq:
            freq[s1[i]] += 1
        else:
            freq[s1[i]] = 1

    for i in range(len(s2)):
        if s2[i] not in freq:
            return 0

        elif freq[s2[i]] == 0:
            return 0

        else:
            freq[s2[i]] -= 1

    return 1


s1 = "listen"
s2 = "silent"

if anagram(s1, s2):
    print("Anagram")
else:
    print("Not Anagram")
```

**Learning:**
- Count character frequencies using a dictionary.
- Decrease frequencies using the second string.
- Check for zero frequency before decrementing.
- Return success only after the complete loop.

**Time Complexity:** O(n)

---

## Q9. Longest Substring Without Repeating Characters

**Input:**
```python
s = "abcabcbb"
```

**Output:**
```python
3
```

**Solution:**
```python
s = "abcabcbb"

last_seen = {}
left = 0
max_length = 0

for right in range(len(s)):
    char = s[right]

    if char in last_seen and last_seen[char] >= left:
        left = last_seen[char] + 1

    current_length = right - left + 1

    if current_length > max_length:
        max_length = current_length

    last_seen[char] = right

print(max_length)
```

**Learning:** Sliding Window + Dictionary.

- `left` tracks the starting index.
- `right` tracks the current index.
- Dictionary stores the last seen index.
- Duplicate characters move the left pointer.
- Window length = `right - left + 1`.

**Time Complexity:** O(n)

---

## Q10. Maximum Sum Subarray — Kadane's Algorithm

**Input:**
```python
numbers = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
```

**Output:**
```python
6
```

**Maximum Subarray:**
```python
[4, -1, 2, 1]
```

**Solution:**
```python
numbers = [-2, 1, -3, 4, -1, 2, 1, -5, 4]

current_sum = 0
max_sum = numbers[0]

for number in numbers:
    current_sum += number

    if current_sum > max_sum:
        max_sum = current_sum

    if current_sum < 0:
        current_sum = 0

print(max_sum)
```

**Learning:**
- Maintain a running sum.
- Update maximum sum whenever a larger sum is found.
- Reset current sum when it becomes negative.
- Initialize `max_sum` with the first element to handle all-negative arrays.

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

---


## Important DSA Patterns Learned

1. **Hashing:** Dictionary lookup and frequency counting.
2. **Two Pointers:** Efficient array traversal and merging.
3. **Sliding Window:** Finding longest valid substring.
4. **Kadane's Algorithm:** Maximum sum contiguous subarray.
5. **In-place Manipulation:** Moving zeroes using swapping.

