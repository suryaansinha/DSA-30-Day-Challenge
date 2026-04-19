# Intuition
We need to merge two sorted lists into one sorted list. The recursive approach is elegant — at each step we just pick the smaller head between the two lists and let recursion handle the rest. The smaller node's next becomes the result of merging the remaining nodes, building the merged list naturally as the recursion unwinds.

# Approach
Base case — if either list is null, return the other list since nothing is left to merge. Otherwise compare head1->val and head2->val. If head1->val <= head2->val, head1 is the smaller node so set head1->next = mergeTwoLists(head1->next, head2) and return head1. Otherwise head2 is smaller so set head2->next = mergeTwoLists(head1, head2->next) and return head2. Each recursive call moves at least one pointer forward so the recursion always terminates.

# Complexity
- Time complexity:
$$O(n + m)$$ — every node from both lists is visited exactly once across all recursive calls, where n and m are the lengths of the two lists

- Space complexity:
$$O(n + m)$$ — recursive call stack depth equals the total number of nodes in both lists in the worst case

# Code
```cpp []
/*
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
    ListNode* mergeTwoLists(ListNode* head1, ListNode* head2) {
        if(head1 == NULL || head2 == NULL){
            return head1 == NULL ? head2 : head1;
        }
        if(head1 -> val <= head2 -> val){
            head1->next = mergeTwoLists(head1->next, head2);
            return head1;
        }
        else{
            head2 -> next = mergeTwoLists(head1, head2->next);
            return head2;
        }
    }
};
```
