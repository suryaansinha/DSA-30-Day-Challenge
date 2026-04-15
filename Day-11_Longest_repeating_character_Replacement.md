# Intuition
To solve this problem, we aim to find the longest substring where we can make all characters the same by replacing at most `k` characters.

Instead of trying all possible replacements, we observe that in any substring, if we know the frequency of the most common character, then the minimum replacements needed is:

(window size - max frequency character)

If this value is ≤ `k`, the substring is valid. So, we try to maximize the window size while keeping it valid.

---

# Approach
We use the sliding window technique along with a frequency array:

1. Initialize:
   - A frequency array `freq[26]` to store counts of characters.
   - Two pointers `left` and `right` for the window.
   - `maxFreq` to store the highest frequency character in the window.
   - `maxLen` to store the result.

2. Expand the window:
   - Move `right` pointer and update frequency.
   - Update `maxFreq` with the maximum frequency in the current window.

3. Check window validity:
   - If `(right - left + 1) - maxFreq > k`, shrink the window from the left.
   - Decrease frequency of the left character and move `left`.

4. Update result:
   - Track the maximum window size using `maxLen`.

---

# Complexity

- **Time Complexity:** O(n)  
  Each character is processed at most twice (once when expanding and once when shrinking).

- **Space Complexity:** O(1)  
  We use a fixed-size frequency array of size 26.

  
# Code
```cpp []
class Solution {
public:
    int characterReplacement(string s, int k) {
        int freq[26] = {0};  // frequency of each char in window
        int left = 0;
        int maxFreq = 0;     
        int maxLen = 0;

        for(int right = 0; right < s.length(); right++) {
            freq[s[right] - 'A']++;

            // update max frequency in window
            maxFreq = max(maxFreq, freq[s[right] - 'A']);

            // window invalid → shrink from left
            // (windowSize - maxFreq) = chars we need to replace
            while((right - left + 1) - maxFreq > k) {
                freq[s[left] - 'A']--;
                left++;
            }

            maxLen = max(maxLen, right - left + 1);
        }

        return maxLen;
    }
};
```
