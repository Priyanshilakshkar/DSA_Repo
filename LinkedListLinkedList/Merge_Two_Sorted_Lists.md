
# 65. Merge Two Sorted Lists

## 📌 Problem Statement

Given the heads of two sorted linked lists, merge them into a single sorted linked list and return the head of the merged list.

The merged list should be created by rearranging the nodes of the original lists.

## 🧪 Example

**Input:**
```text
list1 = [1, 2, 4]
list2 = [1, 3, 4]
```

**Output:**
```text
[1, 1, 2, 3, 4, 4]
```

**Explanation:**

Both linked lists are sorted. Merge their nodes in ascending order to obtain a single sorted linked list.

---

## 1️⃣ Brute Force Approach

### 💡 Intuition

Store all the elements from both linked lists in an array or list, sort them, and then create a new linked list using the sorted elements.

### 🔍 Algorithm

1. Traverse the first linked list and store all its elements.
2. Traverse the second linked list and store all its elements.
3. Sort the collected elements.
4. Create a new linked list using the sorted elements.
5. Return the head of the new linked list.

### 💻 Java Code

```java
import java.util.*;

class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        List<Integer> values = new ArrayList<>();

        while (list1 != null) {
            values.add(list1.val);
            list1 = list1.next;
        }

        while (list2 != null) {
            values.add(list2.val);
            list2 = list2.next;
        }

        Collections.sort(values);

        ListNode dummy = new ListNode(-1);
        ListNode curr = dummy;

        for (int value : values) {
            curr.next = new ListNode(value);
            curr = curr.next;
        }

        return dummy.next;
    }
}
```

### ⏱️ Complexity Analysis

Let `N` be the total number of nodes in both lists.

- **Time Complexity:** `O(N log N)` — Collecting the elements takes `O(N)`, sorting takes `O(N log N)`, and building the new list takes `O(N)`.
- **Space Complexity:** `O(N)` — Extra space is required to store the elements and create the new list.

---

## 2️⃣ Optimal Approach — Two Pointers

### 💡 Intuition

Since both linked lists are already sorted, there is no need to sort their elements again.

Compare the current nodes of both lists and attach the smaller node to the merged list. Move the corresponding pointer forward and repeat until one list becomes empty.

Finally, attach the remaining nodes of the other list.

### 🔍 Algorithm

1. Create a dummy node to simplify list construction.
2. Maintain a pointer `curr` to the last node of the merged list.
3. Compare the current nodes of both lists.
4. Attach the smaller node to `curr.next`.
5. Move the pointer of the selected list forward.
6. Move `curr` forward.
7. When one list becomes empty, attach the remaining nodes of the other list.
8. Return `dummy.next`.

### 💻 Java Code

```java
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode(-1);
        ListNode curr = dummy;

        while (list1 != null && list2 != null) {
            if (list1.val <= list2.val) {
                curr.next = list1;
                list1 = list1.next;
            } else {
                curr.next = list2;
                list2 = list2.next;
            }

            curr = curr.next;
        }

        // Attach the remaining nodes
        if (list1 != null) {
            curr.next = list1;
        } else {
            curr.next = list2;
        }

        return dummy.next;
    }
}
```

### ⏱️ Complexity Analysis

Let `N = n + m`, where `n` and `m` are the lengths of the two linked lists.

- **Time Complexity:** `O(n + m)` — Each node is processed at most once.
- **Space Complexity:** `O(1)` — Only a constant number of pointers are used; existing nodes are reused.

---

## 📊 Approach Comparison

| Criteria | Brute Force | Optimal |
|---|---|---|
| Technique | Collect, sort, rebuild | Two pointers |
| Time Complexity | `O(N log N)` | `O(n + m)` |
| Auxiliary Space | `O(N)` | `O(1)` |
| Reuses Original Nodes | No | Yes |
| Efficiency | Less efficient | More efficient |

## 🧠 Key Concepts Learned

- Singly Linked List
- Two-Pointer Technique
- Dummy Node
- Pointer Manipulation
- Sorted List Merging
- Time and Space Complexity

## ✅ Conclusion

The brute force approach collects and sorts all elements before constructing a new linked list.

The optimal approach takes advantage of the fact that both input lists are already sorted. By comparing their nodes and reusing the original links, we can merge them in `O(n + m)` time and `O(1)` auxiliary space.

**The two-pointer approach is preferred because it is faster and more space-efficient.**

## 🏷️ Tags

`Java` `DSA` `Linked List` `Two Pointers` `Brute Force` `Optimal Approach`
