### 680. Valid Palindrome II (Easy)

https://leetcode.com/problems/valid-palindrome-ii/

```
// Use two pointer from each side to test if is valid palindrome.
// For we can delete at most one elements, we should try delete which side element in to loops.
class Solution {
public:
    bool validPalindrome(string s) {
        for(int i = 0, j = s.size()-1; i <= j; ++i, --j) {
            if (s[i] != s[j]) {
                int i1 = i+1, j1 = j;
                while(i1 <= j1 && s[i1] == s[j1]) ++i1, --j1;
                if (i1 > j1) return true;
                int i2 = i, j2 = j-1;
                while(i2 <= j2 && s[i2] == s[j2]) ++i2, --j2;
                if (i2 > j2) return true;
                return false;
            }
        }
        return true;
    }
};
```
