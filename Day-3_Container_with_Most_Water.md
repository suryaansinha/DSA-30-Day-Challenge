# Intuition
Water stored between two lines is determined by the shorter line and the distance between them — min(height[i], height[j]) × (j - i). Starting with pointers at both ends gives the maximum possible width. Since width shrinks as we move inward, we must try to gain taller heights to compensate. Moving the taller pointer inward is pointless — the water level is already capped by the shorter side. So we always move the shorter pointer inward, as it's the only side that has any chance of increasing the area.


# Approach
Use two pointers i and j starting at both ends of the array. At each step compute the area as min(height[i], height[j]) × (j - i) and update max_area. Then move the shorter pointer inward — increment i if height[i] < height[j], otherwise decrement j. Repeat until the pointers meet.


# Complexity
- Time complexity:
$$O(n)$$ — each element is visited at most once as the two pointers sweep toward each other


- Space complexity:
$$O(1)$$ — only a few integer variables used, no extra data structures


# Code
```cpp []
class Solution {
public:
    int maxArea(vector<int>& height) {
        int max_area = 0;
        int n = height.size();
        int i = 0, j = n-1;
        while(i < j){
            int h = min(height[i], height[j]);
            int area = h*(j-i);
            max_area = max(area, max_area);
            if(height[i]<height[j]){i++;}
            else{j--;}
        }
        return max_area;
    }
};
```
