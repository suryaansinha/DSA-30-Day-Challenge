# Intuition
In Reverse Polish Notation, operators always come after their operands. A stack is the natural fit — whenever we see a number we push it, and whenever we see an operator we pop the top two numbers, apply the operation, and push the result back. By the end of the traversal the stack contains exactly one element — the final answer.

# Approach
Initialize an integer stack s. Iterate through each token — if it is not +, -, *, or / it must be a number, so convert it with stoi and push it. Otherwise pop a (top) and b (second from top) and apply the operator pushing the result back. Note the order matters for subtraction and division — it is always b operator a since b was pushed before a. After the loop return s.top().

# Complexity
- Time complexity:
$$O(n)$$ — single pass through all tokens, each token is processed exactly once

- Space complexity:
$$O(n)$$ — in the worst case all tokens are numbers and get pushed onto the stack before any operator is seen

# Code
```cpp []
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> s;
        for(int i=0;i<tokens.size(); i++) {
            if(tokens[i] != "+" && tokens[i] != "-" && tokens[i] != "*" && tokens[i] != "/"){
                s.push(stoi(tokens[i]));
            }
            else if(tokens[i]=="+"){
                int a = s.top();
                s.pop();
                int b = s.top();
                s.pop();
                s.push(b+a);
            }
            else if(tokens[i]=="-"){
                int a = s.top();
                s.pop();
                int b = s.top();
                s.pop();
                s.push(b-a);
            }
            else if(tokens[i]=="*"){
                int a = s.top();
                s.pop();
                int b = s.top();
                s.pop();
                s.push(b*a);
            }
            else if(tokens[i]=="/"){
                int a = s.top();
                s.pop();
                int b = s.top();
                s.pop();
                s.push(b/a);
            }
        }
        return s.top();
    }
};
```
