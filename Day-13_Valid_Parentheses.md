# Intuition
Every opening bracket must be closed by the same type of bracket in the correct order. A stack is perfect here because it follows LIFO — the most recently opened bracket must be the next one closed. If we see a closing bracket that doesn't match the top of the stack, the string is immediately invalid.

# Approach
Iterate through each character. If it's an opening bracket (, {, or [ push it onto the stack. If it's a closing bracket, first check if the stack is empty — if so return false since there's no opener to match. Otherwise check if the top of the stack is the corresponding opener using three OR conditions. If it matches, pop the stack. If it doesn't match, return false. After the loop, return st.empty() — if the stack still has unmatched openers left it's invalid, otherwise it's valid

# Complexity
- Time complexity:
$$O(n)$$ — single pass through the string, each character is pushed and popped at most once

- Space complexity:
$$O(n)$$ — in the worst case all characters are opening brackets and get pushed onto the stack, e.g. (((((

# Code
```cpp []
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;

        for(int i = 0; i < s.length(); i++) {
            char ch = s[i];

            if(ch == '(' || ch == '{' || ch == '[') {
                st.push(ch);
            }
            else {
                if(st.empty()) return false;

                char top = st.top();

                if((ch == ')' && top == '(') ||
                   (ch == '}' && top == '{') ||
                   (ch == ']' && top == '[')) {
                    st.pop();
                }
                else {
                    return false;  
                }
            }
        }

        return st.empty();  
    }
};
```
