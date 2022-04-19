### 1616. Split Two Strings to Make Palindrome (Medium)

https://leetcode.com/problems/split-two-strings-to-make-palindrome/

```
class Solution {
public:
    bool isPalindrome(const string& a, int i, int j) {
        while (i < j && a[i] == a[j]) {
            ++i;
            --j;
        }
        return i >= j;
    }
    bool check(const string& a, const string& b) {
        int i = 0, j = a.size() - 1;
        while (i < j && a[i] == b[j]) {
            ++i;
            --j;
        }
        return isPalindrome(a, i, j) || isPalindrome(b, i, j);
    }
    bool checkPalindromeFormation(string a, string b) {
        return check(a, b) || check(b, a);
    }
};
```
