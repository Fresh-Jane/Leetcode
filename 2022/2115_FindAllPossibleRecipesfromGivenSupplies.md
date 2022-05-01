### 2115. Find All Possible Recipes from Given Supplies (Medium)

https://leetcode.com/problems/find-all-possible-recipes-from-given-supplies/

```
// Topologic sort
class Solution {
public:
    vector<string> findAllRecipes(vector<string>& recipes, vector<vector<string>>& ingredients, vector<string>& supplies) {
        const int n = recipes.size();
        vector<int> indegree(n, 0);
        unordered_map<string, vector<int>> dependency;
        for (int i = 0; i < n; ++i) dependency[recipes[i]] = {}; 
        for (int i = 0; i < n; ++i) 
            for (int j = 0; j < ingredients[i].size(); ++j) 
                if (dependency.count(ingredients[i][j])) {
                    dependency[ingredients[i][j]].push_back(i);
                    indegree[i]++;
                }
        unordered_set<string> supply_set(supplies.begin(), supplies.end());
        vector<string> res;
        queue<int> q;
        for (int i = 0; i < n; ++i) if (indegree[i] == 0) q.push(i);
        while(!q.empty()) {
            int cur = q.front(); q.pop();
            bool can_create = true;
            for (int i = 0; i < ingredients[cur].size(); ++i) 
                if (!supply_set.count(ingredients[cur][i])) {
                    can_create = false;
                    break;
                }
            if (can_create) {
                res.push_back(recipes[cur]);
                supply_set.insert(recipes[cur]);
                for (int pre : dependency[recipes[cur]]) 
                    if (--indegree[pre] == 0) q.push(pre);
            }
        }
        return res;
    }
};
```
