# Intuition
The maximum depth of a tree is the longest path from the root down to any leaf. At any node, the depth is simply 1 + the maximum of its left and right subtree depths. Recursion naturally captures this — we ask each subtree for its depth, take the larger one, and add 1 for the current node.

# Approach
Base case — if root == NULL return 0 since an empty tree has no depth. Otherwise recursively compute left = maxDepth(root->left) and right = maxDepth(root->right). Return max(left, right) + 1 where the +1 accounts for the current node itself. The recursion unwinds from the leaves upward, bubbling the correct depth back to the root.

# Complexity
- Time complexity:
$$O(n)$$ — every node is visited exactly once through the recursive calls

- Space complexity:
$$O(h)$$ — where h is the height of the tree due to the recursive call stack. $$O(\log n)$$ for a balanced tree and $$O(n)$$ worst case for a skewed tree

## Dry Run
~~~
        3
       / \
      9  20
        /  \
       15   7

maxDepth(3)
├── maxDepth(9)
│   ├── maxDepth(NULL) → 0
│   └── maxDepth(NULL) → 0
│   └── return max(0,0)+1 = 1
│
└── maxDepth(20)
    ├── maxDepth(15)
    │   ├── maxDepth(NULL) → 0
    │   └── maxDepth(NULL) → 0
    │   └── return max(0,0)+1 = 1
    │
    └── maxDepth(7)
        ├── maxDepth(NULL) → 0
        └── maxDepth(NULL) → 0
        └── return max(0,0)+1 = 1
    
    └── return max(1,1)+1 = 2

return max(1,2)+1 = 3 ✅
~~~

# Code
```cpp []
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root==NULL){
            return 0;
        }
        int left = maxDepth(root->left);
        int right = maxDepth(root->right);
        int abs = max(left, right) +1;
        return abs;
    }
};
```
