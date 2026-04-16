# Intuition
The problem requires designing a stack that supports push, pop, top, and retrieving the minimum element in constant time.

A normal stack cannot return the minimum in O(1) without scanning all elements. So, we need a way to **store minimum information along with each element**.

The key idea is:
Instead of storing just values, store a pair:
(value, minimum up to this point)

This way, every element knows the minimum value of the stack at the moment it was pushed.

---

# Approach
We use a stack of pairs:

1. Each element in the stack stores:
   - The value
   - The minimum value at that point

2. Push operation:
   - If the stack is empty, the minimum is the value itself.
   - Otherwise, the new minimum is:
     min(current value, previous minimum)
   - Push `{value, current minimum}`

3. Pop operation:
   - Simply remove the top element.

4. Top operation:
   - Return the first element of the top pair.

5. getMin operation:
   - Return the second element of the top pair.

This ensures all operations run in constant time.

---

# Complexity

- **Time Complexity:** O(1) for all operations  
  (push, pop, top, getMin)

- **Space Complexity:** O(n)  
  We store an extra value (minimum) for each element in the stack.

# Code
```cpp []
class MinStack {
public:
    stack<pair<int,int>> st;
    int minimum = INT_MAX;
    MinStack() {
    }
    
    void push(int val) {
        if(st.empty()) minimum = val;
        else minimum = min(st.top().second,val);
        st.push({val, minimum});
        
    }
    
    void pop() {
        if(!st.empty()) st.pop();
    }
    
    int top() {
        return st.top().first;
    }
    
    int getMin() {
        return st.top().second;
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(val);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```
