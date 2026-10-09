
# 124. Sort a Linked List

## 📌 Problem Statement

Given the head of a singly linked list, sort the linked list in ascending order and return its head.

## 🧪 Example

**Input:**
```text
head = [4, 2, 1, 3]
```

**Output:**
```text
[1, 2, 3, 4]
```

**Explanation:**

The nodes are rearranged so that their values appear in ascending order.

---

## 1️⃣ Brute Force Approach

### 💡 Intuition

Store all the node values in an array, sort the array, and then update the values of the original linked list using the sorted elements.

### 🔍 Algorithm

1. Traverse the linked list and store all node values in an array.
2. Sort the array in ascending order.
3. Traverse the linked list again.
4. Replace each node's value with the corresponding sorted value.
5. Return the original head.

### 💻 Java Code

```java
import java.util.*;

class Solution {
    public ListNode sortList(ListNode head) {
        List<Integer> values = new ArrayList<>();

        ListNode curr = head;

        while (curr != null) {
            values.add(curr.val);
            curr = curr.next;
        }

        Collections.sort(values);

        curr = head;
        int i = 0;

        while (curr != null) {
            curr.val = values.get(i);
            i++;
            curr = curr.next;
        }

        return head;
    }
}
```

### ⏱️ Complexity Analysis

Let `N` be the number of nodes in the linked list.

- **Time Complexity:** `O(N log N)` — Sorting takes `O(N log N)`, and traversing the list takes `O(N)`.
- **Space Complexity:** `O(N)` — An additional array stores all node values.

### ⚠️ Limitation

This approach modifies node values and requires extra memory to store them.

---

## 2️⃣ Optimal Approach — Merge Sort

### 💡 Intuition

Merge Sort is well suited for linked lists because it can sort them efficiently by rearranging pointers without requiring an array.

The approach follows three steps:

1. **Divide:** Find the middle node and split the list into two halves.
2. **Conquer:** Recursively sort both halves.
3. **Merge:** Merge the two sorted halves into one sorted linked list.

### 🔍 Algorithm

1. If the list is empty or contains only one node, return it.
2. Find the middle of the linked list using slow and fast pointers.
3. Split the list into two halves.
4. Recursively sort each half.
5. Merge the two sorted halves using a two-pointer technique.
6. Return the head of the sorted list.

### 💻 Java Code

```java
class Solution {

    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        // Find the middle of the linked list
        ListNode slow = head;
        ListNode fast = head;
        ListNode prev = null;

        while (fast != null && fast.next != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        prev.next = null;

        ListNode left = sortList(head);
        ListNode right = sortList(slow);

        return merge(left, right);
    }

    private ListNode merge(ListNode left, ListNode right) {
        ListNode dummy = new ListNode(-1);
        ListNode curr = dummy;

        while (left != null && right != null) {
            if (left.val <= right.val) {
                curr.next = left;
                left = left.next;
            } else {
                curr.next = right;
                right = right.next;
            }

            curr = curr.next;
        }

        if (left != null) {
            curr.next = left;
        } else {
            curr.next = right;
        }

        return dummy.next;
    }
}
```

### ⏱️ Complexity Analysis

- **Time Complexity:** `O(N log N)` — The list is divided into halves over `log N` levels, and each level processes `N` nodes.
- **Space Complexity:** `O(log N)` — The recursive call stack requires logarithmic space. The merge operation itself uses `O(1)` auxiliary space.

---

## 📊 Approach Comparison

| Criteria | Brute Force | Optimal |
|---|---|---|
| Technique | Array + Sorting | Merge Sort |
| Time Complexity | `O(N log N)` | `O(N log N)` |
| Auxiliary Space | `O(N)` | `O(log N)` |
| Rearranges Links | No | Yes |
| Efficiency | Simple | Preferred for linked lists |

## 🧠 Key Concepts Learned

- Singly Linked List
- Merge Sort
- Slow and Fast Pointers
- Divide and Conquer
- Recursion
- Two-Pointer Technique
- Pointer Manipulation

## ✅ Conclusion

The brute force approach stores node values in an array, sorts them, and writes them back into the list.

The optimal approach uses Merge Sort to divide the linked list into smaller parts, recursively sort them, and merge the results by rearranging pointers.

**Merge Sort is preferred because it achieves `O(N log N)` time complexity while avoiding an additional array.**

## 🏷️ Tags

`Java` `DSA` `Linked List` `Merge Sort` `Recursion` `Divide and Conquer` `Sorting`
