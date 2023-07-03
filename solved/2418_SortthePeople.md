### 2418. Sort the People (Easy)

https://leetcode.com/problems/sort-the-people/description/

```
class Solution {
public:
    vector<string> sortPeople(vector<string>& name, vector<int>& height) {
        const int n = name.size();
        vector<int> id(n);
        for (int i = 0; i < n; ++i) id[i] = i;
        sort(id.begin(), id.end(), [&](int i, int j){
            return height[i] > height[j];
        });
        vector<string> res(n);
        for (int i = 0; i < n; ++i) res[i] = name[id[i]];
        return res;
    }
};
```
