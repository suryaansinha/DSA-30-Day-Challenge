# Intuition
We need the longest substring with no repeated characters. The key insight is to use a sliding window — maintain a window [left, right] that always contains unique characters. As we expand right, if the new character already exists in the window, we shrink from left until the duplicate is removed. This way the window is always valid and we track the maximum length seen.

# Approach
Use an unordered_set to track characters currently in the window. Expand right one character at a time — if s[right] is already in seen, keep erasing s[left] and incrementing left until the duplicate is gone. Then insert s[right] into seen and update max_len with right - left + 1. By the end of the loop max_len holds the answer.


# Complexity
- Time complexity:
$$O(n)$$ — each character is inserted and erased from the set at most once, so despite the nested while loop the total operations across all iterations is still linear


- Space complexity:
$$O(min(n,m))$$ — where m is the size of the character set (at most 128 for ASCII). The seen set never holds more unique characters than exist in the alphabet


# Code
```cpp []
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_set<char> seen;
        int left = 0;
        int max_len = 0;
        for(int right = 0 ; right < s.length(); right++){
            while(seen.count(s[right])){
                seen.erase(s[left]);
                left++;
            }
            seen.insert(s[right]);
            max_len = max(max_len, right - left + 1);
        }        
        return max_len;
    }
};
```
