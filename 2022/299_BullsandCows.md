### 299. Bulls and Cows (Medium)

https://leetcode.com/problems/bulls-and-cows/

```
class Solution {
public:
    string getHint(string secret, string guess) {
        vector<int> sm(10), gm(10);
        const int n = secret.size();
        int a = 0;
        for (int i = 0; i < n; ++i) {
            if (secret[i] == guess[i]) a++;
            else {
                gm[guess[i]-'0']++;
                sm[secret[i]-'0']++;
            }
        }
        int b = 0;
        for (int i = 0; i < 10; ++i)  b += min(sm[i], gm[i]);
        return to_string(a)+'A'+to_string(b)+'B';    
    }
};
```
