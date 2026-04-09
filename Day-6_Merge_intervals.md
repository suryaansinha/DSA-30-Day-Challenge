# Intuition
If we sort intervals by their start time, overlapping intervals will always be adjacent to each other. Then we just walk through once — if the current interval overlaps with the last one in our result (i.e. its start is ≤ the last end), we merge them by extending the end. Otherwise we simply add it as a new interval. Sorting is the key that makes a single pass sufficient.


# Approach
Sort all intervals by start value. Initialize an empty ans vector. For each interval:

If ans is empty → push it directly
Otherwise get a reference v to the last interval in ans:

If intervals[i][0] <= v[1] → they overlap, so merge by updating v[1] = max(v[1], intervals[i][1]). Taking the max handles the case where one interval is completely contained inside another.
Otherwise → no overlap, push the current interval as a new entry



The reference &v = ans.back() is crucial — it directly modifies the last element in ans in place without copying.

# Complexity
- Time complexity:
$$O(n \log n)$$ — dominated by the sort; the single pass through intervals is just $$O(n)$$



- Space complexity:
$$O(n)$$ — the output ans vector stores at most all n intervals in the worst case when no merging occurs


# Code
```cpp []
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> ans;
        for(int i=0; i<intervals.size();i++)
        {
            if(ans.empty()){ans.push_back(intervals[i]);}
            else{
            vector<int> &v = ans.back();
            
            int y = v[1];
            if (intervals[i][0]<=v[1])
            {
                v[1] = max(intervals[i][1], y);
            }
            else
            {
                ans.push_back(intervals[i]);
            }


            }
        }
        return ans;
    }
};
```
