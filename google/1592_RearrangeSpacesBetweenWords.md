### 1592. Rearrange Spaces Between Words (Easy)

https://leetcode.com/problems/rearrange-spaces-between-words/

```
class Solution {
public:
    string reorderSpaces(string text) {
        string word;
        vector<string> words;
        istringstream ss(text);
        while (ss >> word) words.push_back(word);
        
        int num_b = 0;
        for (int i = 0; i < text.size(); ++i) if (text[i] == ' ') num_b++;
        
        string res;
        const int num_w = words.size();
        const int ave = num_w > 1 ? num_b / (num_w - 1) : 0;
        const int left = num_b - (num_w - 1) * ave;
        for (int i = 0; i < words.size(); ++i) {
            res += words[i];
            if (i != words.size() - 1) res += string(ave, ' ');
        }
        res += string(left, ' ');
        return res;
    }
};
```
