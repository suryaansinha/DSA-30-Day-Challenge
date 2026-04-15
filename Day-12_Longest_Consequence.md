# Intuition
The goal is to find the length of the longest sequence of consecutive integers in an unsorted array.

A brute-force approach would involve sorting the array, but that would take O(n log n) time. Since the problem requires O(n), we need a faster way.

The key idea is to use a set for O(1) lookups. For each number, we only try to build a sequence if it is the **start** of a sequence.

A number is the start of a sequence if `(num - 1)` is not present in the set.

From such a starting point, we keep checking for `(num + 1), (num + 2), ...` and count the length of the sequence.

---

# Approach
1. Insert all elements into an unordered set for O(1) lookup.
2. Iterate through each number in the set:
   - Check if `(num - 1)` is NOT in the set.
     - If true, this is the start of a new sequence.
3. From this starting number:
   - Keep incrementing the number and check if the next exists in the set.
   - Count the length of this sequence.
4. Track the maximum sequence length using `globalLen`.

---

# Complexity

- **Time Complexity:** O(n)  
  Each element is processed at most once when expanding sequences.

- **Space Complexity:** O(n)  
  We use an unordered set to store all elements.
  
# Code
```cpp []
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        int n = nums.size();
        if (n == 0) return 0;
        unordered_set<int> st;

        for (int i: nums) st.insert(i);

        int globalLen = 0;
        for (int i: st) {
            if (!st.count(i - 1)) {
                int currLen = 1;
                int currNum = i;
                while (st.count(currNum + 1)) {
                currLen ++;
                currNum ++;
                }
            globalLen = max(currLen, globalLen);
            }
        }
    return globalLen;
    }
};
```
## 💡 Key Insight
Only start counting when the current number is the **beginning** of a sequence.  
This avoids redundant work and ensures O(n) time complexity.
