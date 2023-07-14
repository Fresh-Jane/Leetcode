### 443. String Compression (Medium)

https://leetcode.com/problems/string-compression/description/

```
// Space: O(1)
class Solution {
public:
    int compress(vector<char>& chars) {
        const int n = chars.size();
        int cnt = 1;
        char tmp = chars[0];
        int i = 1, j = 0;
        while(i < n) {
            if (chars[i] == tmp) cnt++;
            else {
                chars[j++] = tmp;
                if (cnt > 1) {
                    int start = j;
                    while(cnt) {
                        chars[j++] = (cnt % 10) + '0';
                        cnt /= 10;
                    }
                    reverse(chars.begin()+start, chars.begin()+j);
                }
                cnt = 1;
                tmp = chars[i];
            }
            i++;
        }
        chars[j++] = tmp;
        if (cnt > 1) {
            int start = j;
            while(cnt) {
                chars[j++] = (cnt % 10) + '0';
                cnt /= 10;
            }
            reverse(chars.begin()+start, chars.begin()+j);
        }
        return j;
    }
};

// Space: O(N)
class Solution {
public:
    int compress(vector<char>& chars) {
        string res;
        int count = 0;
        char pre = 0;
        for (const char c : chars) {
            if (c != pre) {
                if (pre) res += pre;
                if (count > 1) res += to_string(count);
                pre = c;
                count = 1;
            } else {
                count++;
            }
        }
        if (pre) res += pre;
        if (count > 1) res += to_string(count);
        for (int i = 0; i < res.size(); ++i) chars[i] = res[i];
        return res.size();
    }
};
```
