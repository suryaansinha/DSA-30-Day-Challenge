# Intuition
Instead of computing prefix/suffix products, we can compute the total product of all non-zero elements once, then derive each answer using division. Zeros need special handling — if there are two or more zeros, every result is 0. If there is exactly one zero, only the position of that zero gets a non-zero result (the product of everything else). If there are no zeros, each position gets productWithoutZero / nums[i].


# Approach
First pass — count zeros and compute the product of all non-zero elements using *=. Then second pass — for each index:

If nums[i] != 0 → if any zero exists in array, result is 0; otherwise result is productWithoutZero / nums[i]
If nums[i] == 0 → if more than one zero exists, result is 0; otherwise result is productWithoutZero (product of all other elements)



# Complexity
- Time complexity:
$$O(n)$$ — two separate linear passes through the array

- Space complexity:
$$O(1)$$ — only two extra integer variables used, output array does not count


# Code
```cpp []
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();

        int count_zero = 0;
        int productwithoutzero = 1;

        for(int &num : nums){
            if(num==0){count_zero++;}
            else {productwithoutzero *= num;}
        }
        vector<int> result(n);

        for(int i = 0; i < n ; i++){
            int num = nums[i];

            if(num != 0){
                if(count_zero > 0){result[i] = 0;}
                else{result[i] = productwithoutzero/nums[i];}
            }
            else {
                if(count_zero > 1){result[i] = 0;}
                else{result[i] = productwithoutzero;}
            }
        } 
        return result;
    }
};
```
