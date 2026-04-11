# Intuition
In a rotated sorted array, the minimum element is the only element that is smaller than both its neighbors. Since one half of the array is always sorted at any midpoint, we can use binary search to zero in on the unsorted half — that's where the minimum (the rotation pivot) must be hiding.

# Approach
Use binary search with l and r at both ends. At each step calculate mid, prev and next using modular arithmetic to handle wrap-around. If nums[mid] is smaller than both its neighbors, it is the minimum — return mid. Otherwise if the right half is sorted (nums[mid] <= nums[r]), the minimum must be in the left half so move r = mid - 1. Otherwise the left half is sorted and the minimum is in the right half so move l = mid + 1. After the loop return nums[0] as the fallback for a non-rotated array.


# Complexity
- Time complexity:
$$O(\log n)$$ — binary search halves the search space at every step

- Space complexity:
$$O(1)$$ — only a few integer variables used, no extra data structures

# Code
```cpp []
class Solution {
public:
    int findMinIndex(vector<int>& nums) {
        int n = nums.size();
        int l = 0, r = n-1;

        while(l <= r) {
            int m = (l + r) / 2;
            int prev = (m - 1 + n) % n;
            int next = (m + 1) % n;

            if(nums[m] <= nums[prev] && nums[m] <= nums[next])
                return m;
            if(nums[m] <= nums[r]) { r = m - 1; }
            else if(nums[l] <= nums[m]) { l = m + 1; }
        }
        return 0;
    }

    int findMin(vector<int>& nums) {
        int i = findMinIndex(nums);  
        return nums[i];
    }
};
```
