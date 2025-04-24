# Merge Two Sorted Lists

**Link:** [https://leetcode.com/problems/merge-two-sorted-lists/](https://leetcode.com/problems/merge-two-sorted-lists/)

**Difficulty:** Easy  
**Date:** 24/04/2025  
**Language:** C++

---

## 🧠 Problem Description

You are given the heads of two **sorted** linked lists `list1` and `list2`.  
Merge the two lists into one **sorted** list by splicing together the nodes of the first two lists.  
Return the head of the merged linked list.

---

## 💡 Approach

We use a **dummy node** to build the merged list easily.  
We compare nodes from both lists and attach the smaller one to the new list.  
At the end, we attach the remaining part of the non-empty list (if any).

---

## 🔍 Complexity

- **Time:** O(n + m), where n and m are the lengths of the two lists
- **Space:** O(1), as we don't create new nodes, only rearrange pointers

---

## 🧪 Code

```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode dummy(0);
        ListNode* current = &dummy;

        while (list1 && list2) {
            if (list1->val < list2->val) {
                current->next = list1;
                list1 = list1->next;
            } else {
                current->next = list2;
                list2 = list2->next;
            }
            current = current->next;
        }

        current->next = list1 ? list1 : list2;

        return dummy.next;
    }
};
