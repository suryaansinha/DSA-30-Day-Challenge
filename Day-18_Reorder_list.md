# Intuition
The reordered list takes nodes alternately from the front and back of the original list. We can't access the back of a linked list directly, so the trick is to split the list in half, reverse the second half, then interleave both halves together. This combines three fundamental linked list techniques into one solution.

# Approach
Step 1 — Find the middle using slow and fast pointers. Slow moves one step at a time, fast moves two. When fast reaches the end, slow is at the middle. Cut the list there by setting slow->next = nullptr.
Step 2 — Reverse the second half using the standard three-pointer reversal with prev, curr, and backup — exactly like problem 206.
Step 3 — Merge the two halves by alternating nodes. Save first->next and second->next before relinking, point first->next = second and second->next = tmp1, then advance both pointers forward. Repeat until second is null.

# Complexity
- Time complexity:
$$O(n)$$ — three separate linear passes through the list, each O(n), giving O(n) overall

- Space complexity:
$$O(1)$$ — only a constant number of pointers used throughout all three steps, no extra data structures

# Code
```cpp []
class Solution {
public:
    void reorderList(ListNode* head) {
        if(!head || !head->next) return;

        // Step 1: Find middle using slow/fast pointers
        ListNode* slow = head;
        ListNode* fast = head;
        while(fast->next && fast->next->next) {
            slow = slow->next;
            fast = fast->next->next;
        }
        // slow is now at middle

        // Step 2: Reverse second half
        ListNode* prev = nullptr;
        ListNode* curr = slow->next;
        slow->next = nullptr;  // cut the list in half

        while(curr) {
            ListNode* backup = curr->next;
            curr->next = prev;
            prev = curr;
            curr = backup;
        }
        // prev is head of reversed second half

        // Step 3: Merge two halves
        ListNode* first = head;
        ListNode* second = prev;

        while(second) {
            ListNode* tmp1 = first->next;
            ListNode* tmp2 = second->next;

            first->next = second;
            second->next = tmp1;

            first = tmp1;
            second = tmp2;
        }
    }
};
```
