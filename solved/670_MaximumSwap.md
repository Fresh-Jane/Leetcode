### 670. Maximum Swap (Medium)

https://leetcode.com/problems/maximum-swap/

```
class Solution {
public:
    int maximumSwap(int num) {
        string s = to_string(num);
        int maxd = -1, maxi = -1;
        int lefti = -1, righti = -1;
        for (int i = s.size()-1; i >= 0; --i) {
            if (s[i]-'0' > maxd) {
                maxd = s[i]-'0';
                maxi = i;
            }
            if (s[i]-'0' < maxd) {
                lefti = i;
                righti = maxi;
            }
        }
        if (lefti == -1) return num;
        swap(s[lefti], s[righti]);
        return stoi(s);
    }
};
```
