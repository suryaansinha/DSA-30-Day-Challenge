# Intuition
A linked list can only be traversed forward, so reversing it means making each node point to its previous node instead of its next. We can't go back once we move forward, so we need three pointers — rev (previous), curr (current), and backup (next) — to reverse the links one step at a time without losing track of the rest of the list.

# Approach
Initialize rev = nullptr, backup = nullptr, curr = head. At each step save curr->next into backup before overwriting it, then point curr->next to rev to reverse the link, then advance rev = curr and curr = backup. Repeat until curr is null. At that point rev is pointing at the new head of the reversed list so return rev.

# Complexity
- Time complexity:
$$O(n)$$ — every node is visited exactly once as curr traverses the full list

- Space complexity:
$$O(1)$$ — only three pointers used regardless of list size, no extra data structures


# Code
```cpp []
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *rev = nullptr, *backup = nullptr, *curr = head;
        while (curr != nullptr){
            backup = curr->next;
            curr->next = rev;
            rev = curr;
            curr = backup;
        }
    return rev;
    
        
    }
};
```
