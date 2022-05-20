### 716. Max Stack (Easy)

https://leetcode.com/problems/max-stack/

```
class MaxStack {
public:
    MaxStack() { }
    
    void push(int x) {
        st.push_back(x);
        m[x].push_back(prev(st.end()));
    }
    
    int pop() {
        int x = st.back();
        st.pop_back();
        m[x].pop_back();
        if (m[x].empty()) m.erase(x);
        return x;
    }
    
    int top() {
        return st.back();
    }
    
    int peekMax() {
        return m.rbegin()->first;
    }
    
    int popMax() {
        auto it = prev(m.end());
        st.erase(it->second.back());
        it->second.pop_back();
        int x = it->first;
        if (it->second.empty()) m.erase(it);
        return x;
    }
private:
    list<int> st;
    using It = list<int>::iterator;
    map<int, vector<It>> m;
};

/**
 * Your MaxStack object will be instantiated and called as such:
 * MaxStack* obj = new MaxStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->peekMax();
 * int param_5 = obj->popMax();
 */
```
