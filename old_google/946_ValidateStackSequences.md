### 946. Validate Stack Sequences (Medium)

https://leetcode.com/problems/validate-stack-sequences/

```
// Solution 1: simulate using a stack
// Time: O(N), Space: O(N) 
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        stack<int> s;
        int j = 0;
        for (const int x : pushed) {
            s.push(x);
            while (!s.empty() && popped[j] == s.top()) {
                j++;
                s.pop();
            }
        }
        return s.empty();
    }
};

// Solution 2: use pushed as stack
// Time: O(N), Space: O(1)
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        int i = 0, j = 0;
        for (const int x : pushed) {
            pushed[i++] = x;
            while (i > 0 && popped[j] == pushed[i-1]) {
                ++j;
                --i;
            }
        }
        return i == 0;
    }
};
```
