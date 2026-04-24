# Intuition
To invert a binary tree, every node's left and right children need to be swapped — and this must happen at every level of the tree. Recursion is the natural fit here because inverting a tree is just swapping the children at the root, then doing the exact same thing for the left subtree and the right subtree. The problem reduces to itself at every level until we hit null.

# Approach
Base case — if root == NULL return NULL. Otherwise swap root->left and root->right using a temp pointer. Then recursively call invertTree on the new root->left and root->right. Return root. The swap happens before the recursive calls (pre-order), meaning we swap at the current node first then go deeper into both subtrees.

# Complexity
- Time complexity:
$$O(n)$$ — every node in the tree is visited exactly once

- Space complexity:
$$O(h)$$ — where h is the height of the tree, due to the recursive call stack. This is $$O(\log n)$$ for a balanced tree and $$O(n)$$ in the worst case for a skewed tree

# Code
```cpp []
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if(root == NULL){
            return NULL;
        }
    TreeNode* temp = root->left;
    root->left = root->right;
    root->right = temp;

    invertTree(root->left);
    invertTree(root->right);
    return root;
    }
};
```
