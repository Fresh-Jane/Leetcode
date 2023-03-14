### 151. Reverse Words in a String (Medium)

https://leetcode.com/problems/reverse-words-in-a-string/

```
// using STL and space O(N)
class Solution {
public:
    string reverseWords(string s) {
        istringstream in(s);
        string res;
        string line;
        while(in >> line) res = line + ' ' + res;
        res.pop_back();
        return res;
    }
};

// in place change and space O(1)
class Solution {
public:
    string reverseWords(string s) {
        auto start = s.find_first_not_of(' ');
        s.erase(0, start); // just index, not pointer
        auto end = s.find_last_not_of(' ');
        s.erase(end+1);
        reverse(s.begin(), s.end());
        int i = 0, n = s.size();
        while(i < n) {
            int j = i;
            while(j < n && s[j] != ' ') ++j;
            reverse(s.begin()+i, s.begin()+j);
            ++j;
            int k = j;
            while(k < n && s[k] == ' ') ++k;
            if (k != j) {
                s.erase(j, k-j);
                n -= k-j;
            }
            i = j;
        }
        return s;
    }
};
```
