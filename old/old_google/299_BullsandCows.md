### 299. Bulls and Cows (Medium)

https://leetcode.com/problems/bulls-and-cows/

```
class Solution {
public:
    string getHint(string secret, string guess) {
        int bull = 0;
        vector<int> hash_s(10, 0), hash_g(10, 0);
        const int n = secret.size();
        for (int i = 0; i < n; ++i) {
            if (secret[i] == guess[i]) bull++;
            else {
                hash_s[secret[i] - '0']++;
                hash_g[guess[i] - '0']++;
            }
        }
        int cow = 0;
        for (int i = 0; i <= 9; ++i) 
            if (hash_s[i] && hash_g[i]) cow += min(hash_s[i], hash_g[i]);
        return to_string(bull) + "A" + to_string(cow) + "B";
    }
};
```
