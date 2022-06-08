### 277. Find the Celebrity (Medium)

https://leetcode.com/problems/find-the-celebrity/

```
/* The knows API is defined for you.
      bool knows(int a, int b); */
// We can rule out one node each time using knows(a, b). 
// a->b, a not candidate, !a->b, b not candidate
// Verify if the last one left is one celebrity.
// Time: O(N)
// Space: O(1) 
class Solution {
public:
    int findCelebrity(int n) {
        int candidate = 0;
        for (int i = 1; i < n; ++i) 
            if (knows(candidate, i)) candidate = i;
        if (isCelebrity(candidate, n)) return candidate;
        return -1;
    }
    bool isCelebrity(int candidate, int n) {
        for (int i = 0; i < n; ++i) {
            if (i == candidate) continue;
            if (knows(candidate, i) || !knows(i, candidate)) return false;
        }
        return true;
    }
};

// Follow up: there are 2 celebrity
```
