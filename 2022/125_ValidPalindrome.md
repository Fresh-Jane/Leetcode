### 125. Valid Palindrome (Easy)

https://leetcode.com/problems/valid-palindrome/

```
class Solution {
public:
    bool isPalindrome(string s) {
        int l = 0, r = s.size()-1;
        while(l <= r) {
            while(l <= r && !isalnum(s[l])) ++l;
            while(l <= r && !isalnum(s[r])) --r;
            if (l <= r && tolower(s[l]) != tolower(s[r])) return false;
            ++l; --r;
        }
        return true;
    }
};
```
