# LeetCode 234 - Palindrome Linked List

## Problem

Given the head of a singly linked list, determine whether the linked list is a **palindrome**.

A palindrome is a sequence that reads the same forward and backward.

### Example

**Input:**

```text
1 -> 2 -> 2 -> 1
```

**Output:**

```text
true
```

Another example:

**Input:**

```text
1 -> 2
```

**Output:**

```text
false
```

---

## Approach

The linked list cannot be accessed backwards directly because it is a singly linked list.

So, the solution uses three main steps:

1. Find the **middle** of the linked list using the slow and fast pointer technique.
2. Reverse the **second half** of the linked list.
3. Compare the first half with the reversed second half.

If all corresponding values are equal, the linked list is a palindrome.

---

## Algorithm

1. Initialize two pointers:

   * `slow` points to the head.
   * `fast` points to the head.

2. Move:

   * `slow` one step at a time.
   * `fast` two steps at a time.

3. When `fast` reaches the end, `slow` will be around the middle of the list.

4. Reverse the linked list starting from `slow`.

5. Use two pointers:

   * `first` starting from the head.
   * `second` starting from the reversed second half.

6. Compare the values of both pointers.

7. If any values are different, return `false`.

8. If all values match, return `true`.

---

## Dry Run

Consider:

```text
1 -> 2 -> 2 -> 1
```

### Step 1: Find the middle

The `slow` pointer moves one step and `fast` moves two steps.

Eventually:

```text
slow
 ↓
2 -> 1
```

The list can be viewed as:

```text
First half:   1 -> 2
Second half:  2 -> 1
```

### Step 2: Reverse the second half

```text
2 -> 1
```

becomes:

```text
1 -> 2
```

### Step 3: Compare

```text
First:   1 -> 2
Second:  1 -> 2
```

Both values match.

Therefore:

```text
true
```

---

## Complexity

### Time Complexity

```text
O(n)
```

The list is traversed a constant number of times.

### Space Complexity

```text
O(1)
```

No extra array, stack, or linked list is created. The existing nodes are rearranged in place.

---
