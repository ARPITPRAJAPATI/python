

## 1. Reverse Linked List (LC 206)

**Problem:** Given the head of a singly linked list, reverse the list and return the new head.

**Example:**
```text
Input:  1 -> 2 -> 3 -> 4 -> 5
Output: 5 -> 4 -> 3 -> 2 -> 1
```

**Approach:** Walk through the list once. For each node, save its `next`, point it back to the previous node, then move both pointers forward.

```python
def reverse_list(head):
    prev = None
    while head:
        nxt = head.next
        head.next = prev
        prev = head
        head = nxt
    return prev
```

**Complexity:** Time O(n), Space O(1)

**Edge cases:** empty list returns `None`; single node returns itself.

---

## 2. Linked List Cycle (LC 141)

**Problem:** Return `True` if the linked list has a cycle, otherwise `False`.

**Example:**
```text
Input:  3 -> 2 -> 0 -> -4 -> (back to node 2)
Output: True

Input:  1 -> 2 -> None
Output: False
```

**Approach:** Floyd's cycle detection. Move `slow` by 1 step and `fast` by 2 steps. If there is a cycle, `fast` eventually meets `slow`. If `fast` reaches the end, there is no cycle.

```python
def has_cycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow is fast:
            return True
    return False
```

**Complexity:** Time O(n), Space O(1)

**Edge cases:** empty list and single node without a cycle return `False`.

---

## 3. Merge Two Sorted Lists (LC 21)

**Problem:** Merge two sorted linked lists into one sorted list and return its head.

**Example:**
```text
Input:  list1 = 1 -> 2 -> 4,  list2 = 1 -> 3 -> 4
Output: 1 -> 1 -> 2 -> 3 -> 4 -> 4
```

**Approach:** Use a dummy node and a `tail` pointer. Repeatedly attach the smaller of the two current nodes to `tail`. When one list ends, attach the rest of the other list.

```python
def merge_two_lists(a, b):
    dummy = ListNode(0)
    tail = dummy
    while a and b:
        if a.val <= b.val:
            tail.next = a
            a = a.next
        else:
            tail.next = b
            b = b.next
        tail = tail.next
    tail.next = a if a else b
    return dummy.next
```

**Complexity:** Time O(n + m), Space O(1)

**Edge cases:** one or both lists empty.

---

## 4. Remove Nth Node From End of List (LC 19)

**Problem:** Remove the n-th node from the end of the list and return the head.

**Example:**
```text
Input:  1 -> 2 -> 3 -> 4 -> 5, n = 2
Output: 1 -> 2 -> 3 -> 5
```

**Approach:** One pass with two pointers. Move `fast` n steps ahead, then move `fast` and `slow` together until `fast` reaches the last node. `slow.next` is then the node to remove. A dummy node handles removal of the head.

```python
def remove_nth_from_end(head, n):
    dummy = ListNode(0, head)
    fast = slow = dummy
    for _ in range(n):
        fast = fast.next
    while fast.next:
        fast = fast.next
        slow = slow.next
    slow.next = slow.next.next
    return dummy.next
```

**Complexity:** Time O(n), Space O(1)

**Edge cases:** `[1]` with `n = 1` returns an empty list; `[1, 2]` with `n = 2` removes the head and returns `[2]`.

---

## 5. Merge Intervals (LC 56)

**Problem:** Given a list of intervals `[start, end]`, merge all overlapping intervals and return the result.

**Example:**
```text
Input:  [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]

Input:  [[1,4],[4,5]]
Output: [[1,5]]
```

**Approach:** Sort by start. Keep a result list. If the current interval starts before or at the end of the last merged interval, extend that end with `max`. Otherwise start a new interval.

```python
def merge_intervals(intervals):
    intervals.sort(key=lambda x: x[0])
    res = [intervals[0][:]]
    for s, e in intervals[1:]:
        if s <= res[-1][1]:
            res[-1][1] = max(res[-1][1], e)
        else:
            res.append([s, e])
    return res
```

**Complexity:** Time O(n log n) for sorting, Space O(n)

**Edge cases:** touching intervals like `[1,4],[4,5]` merge; one interval fully inside another (`[1,10],[2,3]` gives `[[1,10]]`); unsorted input. Assumes at least one interval.

---

## 6. Fruit Into Baskets (LC 904)

**Problem:** Each element of `fruits` is a fruit type along a row of trees. You have two baskets, each holding only one type. Starting at any tree, pick one fruit from each tree moving right, and stop when a tree's fruit does not fit. Return the maximum number of fruits you can pick. This is the longest subarray with at most 2 distinct values.

**Example:**
```text
Input:  [1, 2, 1]
Output: 3

Input:  [1, 2, 3, 2, 2]
Output: 4      (subarray [2, 3, 2, 2])

Input:  [3,3,3,1,2,1,1,2,3,3,4]
Output: 5      (subarray [1, 2, 1, 1, 2])
```

**Approach:** Sliding window with a frequency dictionary. Expand `right`, count each fruit. If the window has more than 2 distinct types, move `left` forward, decreasing counts and removing a type when its count hits 0. Track the maximum window size. Changing `2` to `k` solves "Longest Substring with K Distinct".

```python
def total_fruit(fruits):
    count = {}
    left = best = 0
    for right, f in enumerate(fruits):
        count[f] = count.get(f, 0) + 1
        while len(count) > 2:
            count[fruits[left]] -= 1
            if count[fruits[left]] == 0:
                del count[fruits[left]]
            left += 1
        best = max(best, right - left + 1)
    return best
```

**Complexity:** Time O(n), Space O(1) (at most 3 keys in the dictionary)

**Edge cases:** all same fruit returns the full length; fewer than 3 distinct types returns the full length.

