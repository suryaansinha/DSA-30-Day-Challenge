# Intuition
To remove the Nth node from the end we first need to know its position from the front. Since we don't know the length upfront, we do a first pass to count the total nodes, then convert the end-based position to a front-based index using position = count - n. Then a second pass walks to the node just before the target and skips it by relinking.

# Approach
First pass — traverse the full list counting nodes into count. Calculate position = count - n which is the 0-indexed position of the node to delete. Pass this to the helper deleteNode. Inside the helper, if position == 0 the head itself must be deleted so return head->next directly. Otherwise walk prev forward position - 1 steps using a for loop so it lands on the node just before the target. After the loop set prev->next = prev->next->next to skip over the target node. Return head.

# Complexity
- Time complexity:
$$O(n)$$ — two passes through the list, first to count all nodes and second to reach the target position, both linear

- Space complexity:
$$O(1)$$ — only a constant number of pointers used, no extra data structures

# Code
```cpp []
class Solution {
    ListNode* deleteNode (ListNode* head, int pos){
if(pos == 0) {
head=head->next;
return head;
}
ListNode* prev=head;
for (int i=0;i<pos-1; i++){
    prev = prev->next;
}
prev->next = prev->next->next;
return head;
}
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* curr = head; 
        int count = 0;
        while(curr!=NULL){
            curr = curr->next; 
            count++;
        }
        int position = (count-n);
        return deleteNode (head, position);

    }
};
```
