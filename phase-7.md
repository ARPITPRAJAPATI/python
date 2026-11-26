# Add Python solutions: Rotate Array (LC 189) and 3Sum (LC 15)

## Summary
Adds Python 3 solutions for two commonly asked array problems, with approach, dry run and complexity. Both were tested on the examples below and on edge cases.

| # | LeetCode | Problem | Topic |
|---|---|---|---|
| 1 | 189 | Rotate Array | Arrays, In-place, Reversal |
| 2 | 15 | 3Sum | Sorting, Two Pointers |

---

## 1. Rotate Array (LC 189)

**Problem:** Given an integer array `nums`, rotate it to the right by `k` steps, where `k` is non-negative.

**Example:**
```text
Input:  nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]

Input:  nums = [-1,-100,3,99], k = 2
Output: [3,99,-1,-100]
```

**Common mistake:** Calling `nums.sort()` is incorrect. Sorting changes the relative order of the elements, but rotation must preserve the original order and only shift the starting point.

**Important first step:** `k = k % n`. Rotating by `n` steps returns the same array, so `k` can be larger than `n`.

### Approach 1: Slicing

Split the array into the last `k` elements and the first `n - k` elements, then join them in swapped order.

```python
class Solution(object):
    def rotate(self, nums, k):
        n = len(nums)
        k = k % n

        nums[:] = nums[n-k:] + nums[:n-k]
```

**Dry run** (`nums = [1,2,3,4,5,6,7]`, `k = 3`):
```text
nums[n-k:]  -> [5, 6, 7]
nums[:n-k]  -> [1, 2, 3, 4]
Result      -> [5, 6, 7, 1, 2, 3, 4]
```

`nums[:] = ...` is used so the original list is modified in place instead of creating a new variable.

### Approach 2: Three Reversals (Optimal)

```python
class Solution(object):
    def rotate(self, nums, k):
        n = len(nums)
        k = k % n

        nums.reverse()

        nums[:k] = reversed(nums[:k])
        nums[k:] = reversed(nums[k:])
```

**Dry run** (`nums = [1,2,3,4,5,6,7]`, `k = 3`):
```text
Initial:                  [1, 2, 3, 4, 5, 6, 7]
Reverse whole array:      [7, 6, 5, 4, 3, 2, 1]
Reverse first k elements: [5, 6, 7, 4, 3, 2, 1]
Reverse remaining:        [5, 6, 7, 1, 2, 3, 4]
```

### Complexity

| Approach | Time | Extra Space |
|---|---|---|
| Slicing | O(n) | O(n) |
| Three reversals | O(n) | O(1) |

**Note:** The slice assignments in Approach 2 create temporary slices in Python, so strictly O(1) extra space needs index-based swapping. The three-reversal idea is the standard optimal technique to learn.

**Edge cases:** `k = 0` and `k = n` leave the array unchanged; `k > n` is handled by `k % n`; single element array stays the same.

---

## 2. 3Sum (LC 15)

**Problem:** Given an integer array `nums`, return all unique triplets `[nums[i], nums[j], nums[k]]` such that `i`, `j`, `k` are different indices and `nums[i] + nums[j] + nums[k] == 0`. The answer must not contain duplicate triplets.

**Example:**
```text
Input:  nums = [-1, 0, 1, 2, -1, -4]
Output: [[-1, -1, 2], [-1, 0, 1]]

Input:  nums = [0, 1, 1]
Output: []

Input:  nums = [0, 0, 0]
Output: [[0, 0, 0]]
```

**Approach:** Sort the array. Fix one number `nums[i]`, then use two pointers `l` (just after `i`) and `r` (at the end) to find pairs that sum to `-nums[i]`.

- If the sum is 0, store the triplet and move both pointers, skipping duplicate values.
- If the sum is less than 0, move `l` right to increase the sum.
- If the sum is greater than 0, move `r` left to decrease the sum.
- Skip duplicate values of `nums[i]` so the same triplet is not added twice.
- If `nums[i] > 0`, stop. All remaining numbers are positive, so the sum cannot be 0.

```python
def three_sum(nums):
    nums.sort()
    res = []
    n = len(nums)

    for i in range(n - 2):
        if nums[i] > 0:
            break
        if i > 0 and nums[i] == nums[i - 1]:
            continue

        l, r = i + 1, n - 1
        while l < r:
            s = nums[i] + nums[l] + nums[r]

            if s == 0:
                res.append([nums[i], nums[l], nums[r]])
                l += 1
                r -= 1
                while l < r and nums[l] == nums[l - 1]:
                    l += 1
                while l < r and nums[r] == nums[r + 1]:
                    r -= 1
            elif s < 0:
                l += 1
            else:
                r -= 1

    return res
```

**Dry run** (`nums = [-1, 0, 1, 2, -1, -4]`):
```text
Sorted: [-4, -1, -1, 0, 1, 2]

i=0 (-4): l=1 (-1), r=5 (2) -> sum -3 < 0 -> l moves ... no pair reaches 4, no triplet
i=1 (-1): l=2 (-1), r=5 (2) -> sum 0  -> add [-1, -1, 2]; l=3, r=4
          l=3 (0),  r=4 (1) -> sum 0  -> add [-1, 0, 1]
i=2 (-1): same as nums[1], skipped (duplicate)
i=3 (0):  l=4 (1),  r=5 (2) -> sum 3 > 0 -> r moves, loop ends

Result: [[-1, -1, 2], [-1, 0, 1]]
```

**Complexity:** Time O(n²) (sorting O(n log n) plus the two-pointer loop for each `i`), Space O(1) extra (ignoring the output list).

**Edge cases:** all zeros (`[0,0,0,0]` returns one triplet `[0,0,0]`); fewer than 3 elements returns `[]`; many duplicates; all positive or all negative returns `[]`.

---

## Testing
- [x] Both solutions run in Python 3 on the examples above
- [x] 3Sum compared against a brute-force solution on 2000 random inputs
- [x] Rotate Array compared against slicing on random inputs, including `k = 0`, `k = n` and `k > n`
- [ ] No automated test suite yet

## Checklist
- [x] Problem, approach, dry run and complexity documented for each solution
- [x] Solutions are self-contained

# Add Python solutions for 10 DSA problems (Strings, Arrays, LinkedList, Stack, Heap, Matrix, DP)

## Summary
Simple Python 3 solutions with a one-line idea and complexity for each. All were run on the examples and edge cases.

| # | LeetCode | Problem | Topic |
|---|---|---|---|
| 1 | 151 | Reverse Words in a String | Strings |
| 2 | 14 | Longest Common Prefix | Strings |
| 3 | 392 | Is Subsequence | Two Pointers |
| 4 | 704 | Binary Search | Searching |
| 5 | 20 | Valid Parentheses | Stack |
| 6 | 643 | Maximum Average Subarray I | Sliding Window |
| 7 | 215 | Kth Largest Element in an Array | Heap |
| 8 | 876 | Middle of the Linked List | LinkedList |
| 9 | 54 | Spiral Matrix | Matrix |
| 10 | 70 | Climbing Stairs | Basic DP |

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

---

## 1. Reverse Words in a String (LC 151)
**Problem:** Reverse the order of words. Remove extra spaces.

**Example:** `"  the sky  is blue "` → `"blue is sky the"`

**Idea:** `split()` breaks the string into words and ignores extra spaces. Reverse the list and join with one space.

```python
def reverse_words(s):
    return " ".join(s.split()[::-1])
```
**Complexity:** Time O(n), Space O(n)

---

## 2. Longest Common Prefix (LC 14)
**Problem:** Find the longest common prefix among an array of strings. Return `""` if none.

**Example:** `["flower","flow","flight"]` → `"fl"`

### Approach 1: Sorting
**Idea:** After sorting, the first and last strings are the two extremes. Whatever they share, every string in between shares too. Compare only those two.

```python
def longest_common_prefix(strs):
    if not strs:
        return ""
    strs.sort()
    first, last = strs[0], strs[-1]
    i = 0
    while i < len(first) and i < len(last) and first[i] == last[i]:
        i += 1
    return first[:i]
```
**Complexity:** Time O(n log n * m), Space O(1) extra

### Approach 2: Character by character
**Idea:** Take each character of the first string and check it against the same position in every other string. Stop at the first mismatch or when a string is too short.

```python
def longest_common_prefix(strs):
    if not strs:
        return ""
    s = ""
    for i in range(len(strs[0])):
        ch = strs[0][i]
        for j in range(1, len(strs)):
            if i >= len(strs[j]) or strs[j][i] != ch:
                return s
        s += ch
    return s
```
`i >= len(strs[j])` is checked first so that `strs[j][i]` never goes out of range (short-circuit `or`).

**Complexity:** Time O(n * m), Space O(1)

**Edge cases:** one string returns itself; no common prefix returns `""`.

---

## 3. Is Subsequence (LC 392)
**Problem:** Return `True` if `s` is a subsequence of `t` (characters in the same order, not necessarily next to each other).

**Example:** `s = "abc", t = "ahbgdc"` → `True`; `s = "axc"` → `False`

**Idea:** Two pointers. Move through `t`; whenever `t[j]` matches `s[i]`, move `i`. If `i` reaches the end of `s`, all characters were found in order.

```python
def is_subsequence(s, t):
    i = j = 0
    while i < len(s) and j < len(t):
        if s[i] == t[j]:
            i += 1
        j += 1
    return i == len(s)
```
**Complexity:** Time O(len(t)), Space O(1)

**Edge cases:** empty `s` returns `True`; empty `t` with non-empty `s` returns `False`.

---

## 4. Binary Search (LC 704)
**Problem:** Given a sorted array and a target, return the index of the target or `-1`.

**Example:** `[-1,0,3,5,9,12]`, target `9` → `4`

**Idea:** Check the middle. If the target is bigger, search the right half, else the left half.

```python
def binary_search(nums, target):
    l, r = 0, len(nums) - 1
    while l <= r:
        m = (l + r) // 2
        if nums[m] == target:
            return m
        if nums[m] < target:
            l = m + 1
        else:
            r = m - 1
    return -1
```
**Complexity:** Time O(log n), Space O(1)

---

## 5. Valid Parentheses (LC 20)
**Problem:** Check if brackets `()[]{}` are closed in the correct order.

**Example:** `"()[]{}"` → `True`; `"(]"` → `False`

**Idea:** Push every opening bracket on a stack. For a closing bracket, the top of the stack must be its matching opening bracket. At the end the stack must be empty.

```python
def is_valid(s):
    pairs = {')': '(', '}': '{', ']': '['}
    st = []
    for c in s:
        if c in pairs:
            if not st or st.pop() != pairs[c]:
                return False
        else:
            st.append(c)
    return not st
```
**Complexity:** Time O(n), Space O(n)

---

## 6. Maximum Average Subarray I (LC 643)
**Problem:** Find the contiguous subarray of length `k` with the maximum average and return that average.

**Example:** `[1,12,-5,-6,50,3]`, `k = 4` → `12.75`

**Idea:** Fixed-size sliding window. Add the new element, remove the old one, keep the best sum. Divide by `k` at the end.

```python
def max_avg(nums, k):
    cur = sum(nums[:k])
    best = cur
    for i in range(k, len(nums)):
        cur += nums[i] - nums[i - k]
        best = max(best, cur)
    return best / k
```
**Complexity:** Time O(n), Space O(1)

---

## 7. Kth Largest Element in an Array (LC 215)
**Problem:** Return the kth largest element (not the kth distinct).

**Example:** `[3,2,1,5,6,4]`, `k = 2` → `5`

**Idea:** `heapq.nlargest(k, nums)` returns the k largest in descending order. The last one is the answer.

```python
import heapq

def kth_largest(nums, k):
    return heapq.nlargest(k, nums)[-1]
```
**Complexity:** Time O(n log k), Space O(k)

---

## 8. Middle of the Linked List (LC 876)
**Problem:** Return the middle node. If there are two middle nodes, return the second one.

**Example:** `1->2->3->4->5` → node `3`; `1->2->3->4` → node `3`

**Idea:** `slow` moves 1 step, `fast` moves 2 steps. When `fast` reaches the end, `slow` is at the middle.

```python
def middle_node(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow
```
**Complexity:** Time O(n), Space O(1)

---

## 9. Spiral Matrix (LC 54)
**Problem:** Return all elements of a matrix in spiral order.

**Example:** `[[1,2,3],[4,5,6],[7,8,9]]` → `[1,2,3,6,9,8,7,4,5]`

**Idea:** Keep four boundaries (top, bottom, left, right). Walk right along the top row, down the right column, left along the bottom row, up the left column, and shrink the boundaries after each side. The two `if` checks stop duplicates when one row or column is left.

```python
def spiral_order(m):
    res = []
    top, bot, left, right = 0, len(m) - 1, 0, len(m[0]) - 1
    while top <= bot and left <= right:
        for j in range(left, right + 1):
            res.append(m[top][j])
        top += 1
        for i in range(top, bot + 1):
            res.append(m[i][right])
        right -= 1
        if top <= bot:
            for j in range(right, left - 1, -1):
                res.append(m[bot][j])
            bot -= 1
        if left <= right:
            for i in range(bot, top - 1, -1):
                res.append(m[i][left])
            left += 1
    return res
```
**Complexity:** Time O(m * n), Space O(1) extra

---

## 10. Climbing Stairs (LC 70)
**Problem:** You can climb 1 or 2 steps at a time. Count the ways to reach step `n`.

**Example:** `n = 3` → `3` (1+1+1, 1+2, 2+1)

**Idea:** Ways(n) = Ways(n-1) + Ways(n-2). This is the Fibonacci pattern, so only the last two values are needed.

```python
def climb_stairs(n):
    a, b = 1, 1
    for _ in range(n):
        a, b = b, a + b
    return a
```
**Complexity:** Time O(n), Space O(1)

---
