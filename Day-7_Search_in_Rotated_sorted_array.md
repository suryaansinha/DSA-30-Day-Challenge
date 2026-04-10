# Intuition
A rotated sorted array always has one sorted half at any midpoint. We identify which half is sorted and check if the target falls within it — if yes search there, if no search the other half.

# Approach
Standard binary search with an extra condition at each step. If nums[left] <= nums[mid], the left half is sorted — check if target is in [nums[left], nums[mid]) and move accordingly. Otherwise the right half is sorted — check if target is in (nums[mid], nums[right]] and move accordingly.

# Complexity
- Time complexity:
$$O(\log n)$$ 

- Space complexity:
$O(1)$

# Code
```cpp []
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size() - 1;

        while(left <= right) {
            int mid = left + (right - left) / 2;

            if(nums[mid] == target)
                return mid;

            if(nums[left] <= nums[mid]) {
                if(nums[left] <= target && target < nums[mid])
                    right = mid - 1;  // search left
                else
                    left = mid + 1;   // search right
            }

            else {

                if(nums[mid] < target && target <= nums[right])
                    left = mid + 1;   // search right
                else
                    right = mid - 1;  // search left
            }
        }

        return -1;
    }
};
```
