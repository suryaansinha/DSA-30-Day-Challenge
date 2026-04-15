# Intuition
A permutation has the exact same character frequencies as the original string — order doesn't matter. So instead of generating all permutations, we slide a fixed-size window of s1.length() across s2 and track how many characters still need to be matched (totalchar). When a character from s2 satisfies a remaining need in freq, totalchar drops. When it hits 0, every character is matched — we found a permutation.


# Approach
Build a frequency array freq[26] from s1 and set totalchar = s1.size(). Slide pointer j across s2 — if s2[j] has remaining frequency in freq (i.e. freq[c]-- > 0), decrement totalchar. If totalchar == 0 return true. Once the window exceeds s1.size(), slide i forward — if the character leaving the window was one we had already "used" (i.e. freq[c]++ >= 0), increment totalchar back since we lost a valid match.

# Complexity
- Time complexity:
$$O(n)$$ — j and i each traverse s2 at most once, where n is the length of s2

- Space complexity:
$$O(1)$$ — fixed size array of 26 characters regardless of input size


# Code
```cpp []
class Solution {
public:
    bool checkInclusion(string s1, string s2) {
        int freq[26]={0};
        for(char c:s1){
            freq[c-'a']++;
        }
        int j=0,i=0, totalchar=s1.size();
        while(j<s2.size()){
            if(freq[s2.at(j++)- 'a']-- >0) {
                totalchar--;
            }
            if(totalchar==0) {
            return true;
            }
        //shifting of window
            if(j-i==s1.size() && freq[s2.at (i++) - 'a']++ >=0) {
            totalchar++;
            }
        }
        return false;
    }
};
```
