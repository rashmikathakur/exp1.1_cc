# LeetCode 328 - Odd Even Linked List

## Problem

Given the head of a singly linked list, group all the nodes at **odd positions** together followed by the nodes at **even positions**.

The relative order of the nodes within the odd and even groups should be maintained.

### Important

**Odd and even refer to the position of the node, not its value.**

For example:

```text
1 -> 2 -> 3 -> 4 -> 5
```

Positions:

```text
1st -> Odd
2nd -> Even
3rd -> Odd
4th -> Even
5th -> Odd
```

So the output is:

```text
1 -> 3 -> 5 -> 2 -> 4
```

---

## Approach

We maintain two separate linked-list chains:

* `odd` for nodes at odd positions
* `even` for nodes at even positions

We also store the first even node using `evenHead`.

Initially:

```text
odd = 1
even = 2
evenHead = 2
```

Then we rearrange the `next` pointers so that:

```text
Odd chain:  1 -> 3 -> 5
Even chain: 2 -> 4
```

Finally, we connect the end of the odd chain to the beginning of the even chain.

```text
1 -> 3 -> 5 -> 2 -> 4
```

---

## Algorithm

1. If the list is empty or contains only one node, return `head`.

2. Set:

   * `odd = head`
   * `even = head->next`
   * `evenHead = even`

3. While `even` and `even->next` are not `nullptr`:

   * Connect the current odd node to the next odd node.
   * Move `odd` forward.
   * Connect the current even node to the next even node.
   * Move `even` forward.

4. Connect the last odd node to `evenHead`.

5. Return `head`.

---

## Dry Run

Consider:

```text
1 -> 2 -> 3 -> 4 -> 5
```

### Initial State

```text
odd       = 1
even      = 2
evenHead  = 2
```

### First Iteration

Connect `1` to `3`:

```text
1 -> 3
```

Move `odd` to `3`.

Then connect `2` to `4`:

```text
2 -> 4
```

Move `even` to `4`.

Now:

```text
Odd:   1 -> 3
Even:  2 -> 4
```

### Second Iteration

Connect `3` to `5`:

```text
1 -> 3 -> 5
```

The even chain becomes:

```text
2 -> 4
```

Now the odd chain ends at `5`.

Finally:

```cpp
odd->next = evenHead;
```

This connects:

```text
1 -> 3 -> 5 -> 2 -> 4
```

### Final Output

```text
1 -> 3 -> 5 -> 2 -> 4
```

---

## Why Do We Need `evenHead`?

The `even` pointer keeps moving forward:

```text
2 -> 4 -> nullptr
```

After the loop, `even` may become `nullptr`.

Therefore, we store the first even node separately:

```cpp
ListNode* evenHead = even;
```

This allows us to connect the odd list to the beginning of the even list at the end:

```cpp
odd->next = evenHead;
```

---

## Key Pointer Operations

### 1. Connect odd nodes

```cpp
odd->next = even->next;
```

This skips the current even node and connects the current odd node to the next odd node.

### 2. Move odd pointer

```cpp
odd = odd->next;
```

### 3. Connect even nodes

```cpp
even->next = odd->next;
```

This connects the current even node to the next even node.

### 4. Move even pointer

```cpp
even = even->next;
```

### 5. Join both lists

```cpp
odd->next = evenHead;
```

---

## Complexity

### Time Complexity

```text
O(n)
```

Each node is processed a constant number of times.

### Space Complexity

```text
O(1)
```

No new linked-list nodes are created. The existing `next` pointers are rearranged.

---
