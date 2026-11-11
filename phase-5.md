
# Q1. First Non-Repeating Character

### Problem

Given a string, find the first character that appears only once.

### Concept: HashMap / Dictionary

A dictionary stores each character as a key and its frequency as a value.

Example:

```python
s = "aabbcde"
```

Frequency dictionary:

```python
{
    'a': 2,
    'b': 2,
    'c': 1,
    'd': 1,
    'e': 1
}
```

Now traverse the original string again. The first character whose frequency is 1 is the answer.

**Important:** We use two traversals because a character's frequency must be known before deciding whether it is non-repeating.

### Complexity

- Time: O(n)
- Space: O(k), where k is the number of distinct characters.

---

# Q2. Subarray Sum Equals K

### Problem

Given an array and a target K, count the number of continuous subarrays whose sum equals K.

Example:

```python
numbers = [1, 2, 3, 2, 1]
target = 5
```

Answer: 2

Valid subarrays:

- [2, 3] = 5
- [3, 2] = 5

## Approach 1: Sliding Window

This approach works when all array elements are non-negative.

```python
numbers = [1, 2, 3, 2, 1]
target = 5

l = 0
i = 0
sum = 0
count = 0

while i < len(numbers):

    sum = sum + numbers[i]

    while sum > target:
        sum = sum - numbers[l]
        l += 1

    if sum == target:
        count += 1

    i += 1

print(count)
```

### How it works

- `i` expands the window by adding elements.
- `l` shrinks the window when the sum becomes greater than the target.
- When the current window sum equals target, increase count.

**Limitation:** Sliding window does not work reliably with negative numbers because adding an element may decrease the sum.

## Approach 2: Prefix Sum + HashMap

This approach also works with negative numbers.

```python
n = [1, 2, 3, 2, 1]

prefix_sum = 0
count = 0
freq = {0: 1}
target = 5

for i in range(len(n)):

    prefix_sum += n[i]

    required = prefix_sum - target

    if required in freq:
        count += freq[required]

    if prefix_sum in freq:
        freq[prefix_sum] += 1
    else:
        freq[prefix_sum] = 1

print(count)
```

### Important concepts

**1. Prefix Sum**

Prefix sum means the sum of all elements from the beginning up to the current index.

For:

```python
n = [1, 2, 3, 2, 1]
```

Prefix sums:

```text
Index:       0   1   2   3   4
Element:     1   2   3   2   1
Prefix Sum:  1   3   6   8   9
```

**2. Why do we use `freq = {0: 1}`?**

It represents an empty prefix with sum zero, occurring once.

This helps count subarrays that start from index 0.

**3. Why `prefix_sum - target`?**

Suppose:

```text
Current prefix sum = 6
Target = 5
Required previous prefix sum = 6 - 5 = 1
```

If prefix sum 1 occurred earlier, the elements after that occurrence up to the current index sum to 5.

**4. Why store frequency?**

The same prefix sum can occur multiple times. Each occurrence can create another valid subarray.

Therefore, we add its frequency to the answer instead of simply adding 1.

### Complexity

- Time: O(n)
- Space: O(n)

---

# Q3. Count Subarrays With Equal 0s and 1s

### Problem

Count continuous subarrays containing an equal number of zeros and ones.

Example:

```python
n = [0, 1, 0, 1, 1, 0]
```

Answer: 7

### Concept: Convert 0 to -1

We convert:

- 0 → -1
- 1 → +1

Now a subarray with equal zeros and ones will have a sum of zero.

Example:

```text
[0, 1, 0, 1]

[-1, 1, -1, 1]

Sum = 0
```

We can use Prefix Sum + HashMap to count all zero-sum subarrays.

### Core logic

```python
freq = {0: 1}
prefix_sum = 0
count = 0

for x in n:

    if x == 0:
        prefix_sum -= 1
    else:
        prefix_sum += 1

    if prefix_sum in freq:
        count += freq[prefix_sum]

    if prefix_sum in freq:
        freq[prefix_sum] += 1
    else:
        freq[prefix_sum] = 1

print(count)
```

### Why does this work?

If the same prefix sum appears at two different positions, the elements between those positions have a sum of zero.

Since zero and one were converted to -1 and +1, that means the subarray has equal numbers of zeros and ones.

### Complexity

- Time: O(n)
- Space: O(n)

---

# Q4. Longest Consecutive Sequence

### Problem

Find the length of the longest sequence of consecutive numbers in an unsorted array.

Example:

```python
n = [100, 4, 200, 1, 3, 2, 3, 4, 5, 6, 7, 8]
```

Answer: 8

The longest consecutive sequence is:

```text
1, 2, 3, 4, 5, 6, 7, 8
```

## Approach 1: Sorting

Sort the array and count consecutive elements.

However, sorting takes O(n log n).

## Approach 2: Set

A set provides average O(1) lookup.

### Important logic

Only start counting from a number if its previous number does not exist.

For example:

```text
1 → previous number 0 does not exist → start
2 → previous number 1 exists → don't start
3 → previous number 2 exists → don't start
```

This prevents repeatedly counting the same sequence.

### Code

```python
n = [100, 4, 200, 1, 3, 2, 3, 4, 5, 6, 7, 8]

s = set(n)
longest = 0

for num in s:

    if num - 1 not in s:

        current = num
        count = 1

        while current + 1 in s:
            current += 1
            count += 1

        longest = max(longest, count)

print(longest)
```

### Complexity

- Time: O(n) average
- Space: O(n)

---

# Q5. Longest Subarray With Sum 0

### Problem

Find the length of the longest continuous subarray whose sum is zero.

Example:

```python
n = [1, 2, -3, 3, -1, 2]
```

Answer: 5

Longest zero-sum subarray:

```text
[1, 2, -3, 3, -1]
```

Sum = 0

### Concept: Prefix Sum + HashMap

Unlike Q2, here we need the longest length, not the number of valid subarrays.

Therefore, we store:

```text
Prefix Sum → First Occurrence Index
```

### Code

```python
n = [1, 2, -3, 3, -1, 2]

prefix_sum = 0
max_length = 0

freq = {0: -1}

for i in range(len(n)):

    prefix_sum += n[i]

    if prefix_sum in freq:
        length = i - freq[prefix_sum]
        max_length = max(max_length, length)

    else:
        freq[prefix_sum] = i

print(max_length)
```

### Why store the index?

Suppose a prefix sum appears at index 2 and again at index 4.

```text
Index:       0   1   2   3   4
Array:       1   2  -3   3  -1
Prefix:      1   3   0   3   2
```

The prefix sum 3 appears at index 1 and index 3.

The elements between these positions are:

```text
Index 2 to 3 → [-3, 3]
```

Their sum is zero.

Length:

```text
Current Index - Previous Index
3 - 1 = 2
```

### Why initialize `freq = {0: -1}`?

This handles zero-sum subarrays that begin at index 0.

For example, if the prefix sum becomes zero at index 2:

```text
Length = 2 - (-1) = 3
```

So the subarray from index 0 to index 2 has length 3.

### Important rule

We store only the FIRST occurrence of each prefix sum.

We do not overwrite it because an earlier index produces a longer subarray.

### Complete dry run

Input:

```python
n = [1, 2, -3, 3, -1, 2]
```

Initial values:

```text
prefix_sum = 0
max_length = 0
freq = {0: -1}
```

| Index | Element | Prefix Sum | Action                  | Max Length |
| ----- | ------: | ---------: | ----------------------- | ---------: |
| 0     |       1 |          1 | Store 1 → 0             |          0 |
| 1     |       2 |          3 | Store 3 → 1             |          0 |
| 2     |      -3 |          0 | Found at -1; length = 3 |          3 |
| 3     |       3 |          3 | Found at 1; length = 2  |          3 |
| 4     |      -1 |          2 | Store 2 → 4             |          3 |
| 5     |       2 |          4 | Store 4 → 5             |          3 |

This particular table has a correction to make: the longest subarray is actually found by the repeated prefix sum 3 at indices 1 and 3, giving length 2, while prefix sum 0 at index 2 gives length 3. The maximum for this input is therefore **3**, not 5.

The zero-sum subarray `[1, 2, -3]` has length 3.

### Complexity

- Time: O(n)
- Space: O(n)

---

# Q6. Product of Array Except Self

### Problem

For each index, calculate the product of all array elements except the element at that index.

Example:

```python
n = [1, 2, 3, 4]
```

Output:

```text
[24, 12, 8, 6]
```

### First approach: Total product / current element

We can calculate the product of all elements and divide by the current element.

But the standard problem asks us to solve it without division.

### Optimized approach: Left Product + Right Product

For every index:

```text
Answer[i] = Left Product[i] * Right Product[i]
```

**Left product:** Product of all elements before the current index.

**Right product:** Product of all elements after the current index.

### Code

```python
n = [1, 2, 3, 4]

left = [None] * len(n)
left[0] = 1

left_prod = 1

for i in range(1, len(n)):
    left_prod = n[i-1] * left_prod
    left[i] = left_prod

right = [None] * len(n)
right[-1] = 1

right_prod = 1

for i in range(len(n)-2, -1, -1):
    right_prod = n[i+1] * right_prod
    right[i] = right_prod

result = [None] * len(n)

for i in range(len(n)):
    result[i] = left[i] * right[i]

print(result)
```

### Dry Run

Original array:

```text
[1, 2, 3, 4]
```

Left product:

```text
[1, 1, 2, 6]
```

Right product:

```text
[24, 12, 4, 1]
```

Final calculation:

```text
Index 0: 1  × 24 = 24
Index 1: 1  × 12 = 12
Index 2: 2  × 4  = 8
Index 3: 6  × 1  = 6
```

Final output:

```text
[24, 12, 8, 6]
```

### Important learning

The order of updating variables matters.

For left product:

```python
left_prod = n[i-1] * left_prod
left[i] = left_prod
```

We update the product first, then store it.

### Complexity

- Time: O(n)
- Space: O(n)

---

# Q7. Majority Element

### Problem

Find the element that appears more than n/2 times.

Example:

```python
n = [2, 2, 1, 1, 2, 2, 2]
```

Answer: 2

### Concept: Frequency Dictionary

We maintain a dictionary containing each element and its frequency.

### Code

```python
n = [2, 2, 1, 1, 2, 2, 2]

dict = {}

for i in range(len(n)):

    if n[i] in dict:
        dict[n[i]] += 1

        if dict[n[i]] > len(n)/2:
            print(n[i])
            break

    else:
        dict[n[i]] = 1
```

### Dry Run

```text
2 → frequency 1
2 → frequency 2
1 → frequency 1
1 → frequency 2
2 → frequency 3
2 → frequency 4
```

Array length = 7

Majority threshold:

```text
7 / 2 = 3.5
```

When frequency of 2 becomes 4:

```text
4 > 3.5
```

Therefore, 2 is the majority element.

### Complexity

- Time: O(n)
- Space: O(n)

---

# Q8. Pivot Index

### Problem

Find an index where the sum of elements on the left equals the sum of elements on the right.

Example:

```python
n = [1, 7, 3, 6, 5, 6]
```

Answer: 3

At index 3:

```text
Left Sum  = 1 + 7 + 3 = 11
Right Sum = 5 + 6 = 11
```

### Approach: Left Sum Array + Right Sum Array

We create two arrays:

- `left[i]`: Sum of all elements before index i.
- `right[i]`: Sum of all elements after index i.

### Code

```python
n = [1, 7, 3, 6, 5, 6]

left = [None] * len(n)
left[0] = 0

left_prod = 0

for i in range(1, len(n)):
    left_prod = n[i-1] + left_prod
    left[i] = left_prod

right = [None] * len(n)
right[-1] = 0

right_prod = 0

for i in range(len(n)-2, -1, -1):
    right_prod = n[i+1] + right_prod
    right[i] = right_prod

for i in range(len(n)):

    if right[i] == left[i]:
        print(i)
        break
```

### Dry Run

Left array:

```text
[0, 1, 8, 11, 17, 22]
```

Right array:

```text
[27, 20, 17, 11, 6, 0]
```

Compare:

```text
Index 0: 0  != 27
Index 1: 1  != 20
Index 2: 8  != 17
Index 3: 11 == 11
```

Answer = 3

### Complexity

- Time: O(n)
- Space: O(n)

---

# Q9. Sort Colors – Dutch National Flag Algorithm

### Problem

Sort an array containing only 0, 1 and 2 without using `sort()` or `sorted()`.

Example:

```python
n = [2, 0, 2, 1, 1, 0]
```

Output:

```text
[0, 0, 1, 1, 2, 2]
```

### Concept: Three Pointers

We use three pointers:

```text
low = 0
mid = 0
high = len(n) - 1
```

They divide the array into four regions:

```text
0 to low-1       → All zeros
low to mid-1     → All ones
mid to high      → Unprocessed elements
high+1 to end    → All twos
```

### Code

```python
n = [2, 0, 2, 1, 1, 0]

low = 0
mid = 0
high = len(n) - 1

while mid <= high:

    if n[mid] == 0:

        n[low], n[mid] = n[mid], n[low]

        low += 1
        mid += 1

    elif n[mid] == 1:

        mid += 1

    else:

        n[mid], n[high] = n[high], n[mid]

        high -= 1

print(n)
```

### Three conditions

**Case 1: Current element is 0**

```python
n[low], n[mid] = n[mid], n[low]
low += 1
mid += 1
```

We move zero to the beginning.

Both pointers move because the swapped element at `mid` is already known to be a 1 or a 0 in the processed region.

**Case 2: Current element is 1**

```python
mid += 1
```

One is already in the correct middle region.

**Case 3: Current element is 2**

```python
n[mid], n[high] = n[high], n[mid]
high -= 1
```

We move 2 to the end.

**Important:** We do not increment `mid` here because the element swapped from `high` has not been checked yet.

### Complexity

- Time: O(n)
- Space: O(1)

---

# Q10. Container With Most Water

### Problem

Given an array where each element represents the height of a vertical line, find the maximum water area between two lines.

Example:

```python
height = [1, 8, 6, 2, 5, 4, 8, 3, 7]
```

Expected answer:

```text
49
```

### Formula

```text
Width = right - left

Water Height = min(height[left], height[right])

Area = Width * Water Height
```

### Initial attempt

```python
height = [1, 8, 6, 2, 5, 4, 8, 3, 7]

j = len(height)-1
min_height = 0
maxy = 0

for i in range(0, len(height)):

    width = j-i
    min_height = min(height[i], height[j])

    maxy = max(maxy, width * min_height)

print(maxy)
```

### What was missing?

The logic for calculating area was correct.

However, `j` remained fixed at the last index. This means we only checked pairs involving the last line, not all useful pairs.

### Correct approach: Two Pointers

```python
height = [1, 8, 6, 2, 5, 4, 8, 3, 7]

i = 0
j = len(height) - 1

maxy = 0

while i < j:

    width = j - i

    min_height = min(height[i], height[j])

    maxy = max(maxy, width * min_height)

    if height[i] < height[j]:
        i += 1
    else:
        j -= 1

print(maxy)
```

### Why move the smaller pointer?

The smaller height limits how much water can be stored.

If we move the taller pointer, the width decreases but the limiting smaller height remains unchanged. That cannot produce a better area.

Therefore, we move the pointer with the smaller height to search for a taller line.

### Complexity

- Time: O(n)
- Space: O(1)

**Status:** Approach understood; implementation and independent dry run still need practice.

---


| Concept                    | Questions      |
| -------------------------- | -------------- |
| Dictionary / Frequency Map | Q1, Q2, Q3, Q7 |
| Prefix Sum                 | Q2, Q3, Q5     |
| Prefix Sum + Frequency     | Q2, Q3         |
| Prefix Sum + First Index   | Q5             |
| Set                        | Q4             |
| Left and Right Product     | Q6             |
| Left and Right Sum         | Q8             |
| Three Pointers             | Q9             |
| Two Pointers               | Q10            |
| Sliding Window             | Q2             |

## Most Important Learnings

1. **Frequency vs First Index:** For counting subarrays, store prefix sum frequency. For longest zero-sum subarray, store the first index.
2. **Prefix Sum:** Repeated prefix sums indicate a zero-sum subarray between their positions.
3. **Set:** Useful for fast existence checks and removing duplicates.
4. **Two Pointers:** Can reduce nested loops to a single traversal when the pointer movement is logically justified.
5. **Three Pointers:** Dutch National Flag uses three regions to sort 0, 1 and 2 in one pass.
6. **Left and Right Arrays:** Useful when the answer at each index depends on elements on both sides.
7. **Update Order:** Updating a variable before storing its value can be important in prefix/product calculations.

---
