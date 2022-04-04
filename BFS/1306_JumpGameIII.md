### 1306. Jump Game III (Medium)

https://leetcode.com/problems/jump-game-iii/

```
// DFS
class Solution {
public:
    bool canReach(vector<int>& arr, int start) {
        if (start >= 0 && start < arr.size() && arr[start] >= 0) {
            if (arr[start] == 0) return true;
            arr[start] = -arr[start];
            return canReach(arr, start + arr[start]) || canReach(arr, start - arr[start]);
        }
        return false;
    }
};
```
