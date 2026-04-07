# Intuition
We need to find all unique triplets that sum to zero. A brute force O(n³) check of all triplets works but is too slow. The key insight is that if we sort the array first, we can fix one element a = nums[i] and reduce the problem to finding two numbers in the rest of the array that sum to -a — exactly like Two Sum II. Sorting also makes it easy to skip duplicates to avoid repeating triplets in the result.


# Approach
Sort the array first. Then iterate through each element nums[i] as the fixed first element a, and use two pointers j = i+1 and k = n-1 to find pairs that sum to t = -a.
At each step of the two pointer loop:

If nums[j] + nums[k] == t → valid triplet, add it, then skip duplicate values of both j and k
If nums[j] + nums[k] < t → sum too small, increment j
If nums[j] + nums[k] > t → sum too large, decrement k

Also skip duplicate values of i at the outer loop level to avoid duplicate triplets entirely.

# Complexity
- Time complexity:
$$O(n^2)$$ — sorting is O(n log n), and for each of the n elements we run a two pointer sweep in O(n), giving O(n²) overall


- Space complexity:
$$O(1)$$ — ignoring the output array, no extra data structures are used beyond the pointers


# Code
```cpp []
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {

        // a+b+c = 0
        sort(nums .begin(), nums. end()) ; 
        vector<vector<int>>ans;
        int n=nums.size();

    for (int i=0;i<n;i++){
        int a=nums[i];
        int t=-a; 
        int j=i+1; 
        int k=n-1;
        while(j<k){
            if(nums[j]+nums[k]==t){
            ans.push_back({nums[i], nums[j], nums[k]});
            while(j<k && nums[j]==nums[j+1])j++;
            while(j<k && nums[k]==nums[k-1])k--;
            j++;
            k--;
        }
        else if (nums[j]+nums[k]<t)j++;
        else k--;

    }
    while(i+1<n && nums[i]==nums[i+1])i++;
    }
    return ans;
    }
};
```
