## Description
Given an integer array nums, return true if any value appears more than once in the array, otherwise return false.


```
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        set<int> set;
        for (int ele: nums){
            set. insert (ele);
        }
        return (int) set. size() != (int) nums. size();
    }
};
```
