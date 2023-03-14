### 68. Text Justification (Hard)

https://leetcode.com/problems/text-justification/

```
Let me double check the question I've got is correct. 

We can scan the words, generate new lines under the rule and push them into the result array.

For each new line, we can use one vector of string to save the words and one integer to save the minimum length of the existing words. 
If adding new words length and 1 space, the minimum length won't exceed the maxWidth, we can add one more word in the current line.
Given all words in one line, we should justify the spaces between them. There are two conditions:
If only one word or the final word is in this line, we should pad all extra spaces in the end of line.
Otherwise, we should average pad the extra spaces in each slots.

The time complexity is O(N), where N is the number of words.   

Could I implement it first, go through the codes with some test cases to explain more details?
```
```
class Solution {
public:
    vector<string> fullJustify(vector<string>& words, int maxWidth) {
        vector<string> res;
        int i = 0, n = words.size();
        while(i < n) {
            vector<string> cur;
            int len = words[i].size();
            cur.push_back(words[i++]);
            while(i < n && len + (int)words[i].size() + 1 <= maxWidth) {
                len += words[i].size() + 1;
                cur.push_back(words[i++]);
            }
            int extras = maxWidth - len;
            int slots = cur.size() - 1;
            string r = cur[0];
            if (slots == 0 || i == n) {
                for (int j = 1; j < (int)cur.size(); ++j)
                    r += ' ' + cur[j];
                if ((int)r.size() < maxWidth) r += string(maxWidth-r.size(), ' ');
            } else {
                int spaces = 1 + extras / slots;
                extras %= slots;
                for (int j = 1; j < (int)cur.size(); ++j)
                    r += string(spaces + (extras-- > 0 ? 1 : 0), ' ') + cur[j];
            }
            res.push_back(r);
        }
        return res;
    }
};
```
