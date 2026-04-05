# Intuition
The key observation is that a negative running sum is never worth keeping. At each element, we ask: "Is it better to start a fresh subarray here, or extend the previous one?" If the running sum has gone negative, starting fresh always gives a better result. We track the global maximum throughout this single pass.


# Approach
We use Kadane's Algorithm with two variables — currentSum and maxSum, both initialized to nums[0] to handle all-negative arrays correctly.
At each index i (starting from 1), we decide:

If currentSum + nums[i] > nums[i] → extend the subarray
Otherwise → start a new subarray from nums[i]

This simplifies to currentSum = max(nums[i], currentSum + nums[i]).
After updating currentSum, we update maxSum if currentSum is larger. After one full pass, maxSum holds the answer.


# Complexity
- Time complexity:
$$O(n)$$ — single pass through the array

- Space complexity:
$$O(1)$$ — only two integer variables used, no extra space


# Code
```cpp []
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int currentSum = nums[0];
        int maxSum = nums[0];

        for (int i = 1; i < nums.size(); i++) {
            // Either extend previous subarray or start new one
            currentSum = max(nums[i], currentSum + nums[i]);
            
            // Track global maximum
            maxSum = max(maxSum, currentSum);
        }

        return maxSum;
    }
};
```
