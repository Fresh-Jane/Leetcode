### 97. Interleaving String (Medium)

https://leetcode.com/problems/interleaving-string/

```
// Time: O(l1*l2)
// Space: O(l1*l2)
class Solution {
public:
    bool isInterleave(string s1, string s2, string s3) {
        const int l1 = s1.size(), l2 = s2.size(), l3 = s3.size();
        if (l3 != l1 + l2) return false;
        bool match[l1+1][l2+1];
        memset(match, false, sizeof(match));
        match[0][0] = true;
        for(int i = 1; i <= l1; ++i) 
            if (s1[i-1] == s3[i-1]) match[i][0] = true;
            else break;
        for(int i = 1; i <= l2; ++i) 
            if (s2[i-1] == s3[i-1]) match[0][i] = true;
            else break;
        for (int i = 1; i <= l1; ++i) 
            for (int j = 1; j <= l2; ++j) 
                match[i][j] = (match[i-1][j] && s1[i-1] == s3[i+j-1]) ||
                              (match[i][j-1] && s2[j-1] == s3[i+j-1]);
        return match[l1][l2];
    }
};
```
