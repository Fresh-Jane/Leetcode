### 2246. Longest Path With Different Adjacent Characters (Hard)

https://leetcode.com/problems/longest-path-with-different-adjacent-characters/

```
// DFS
// Time: O(N)
// Space: O(N)
class Solution {
public:
    int longestPath(vector<int>& parent, string s) {
        const int n = parent.size();
        vector<vector<int>> children(n);
        for (int i = 1; i < n; ++i) children[parent[i]].push_back(i);
        int longest_path = 1;
        dfs(0, children, s, longest_path);
        return longest_path;
    }

    int dfs(int current_node, const vector<vector<int>>& children, const string& s, int& longest_path) {
        int longest = 0, second = 0;
        for (int child : children[current_node]) {
            int longest_from_child = dfs(child, children, s, longest_path);
            if (s[child] == s[current_node]) continue;
            if (longest_from_child > longest) {
                second = longest;
                longest = longest_from_child;
            } else if (longest_from_child > second) {
                second = longest_from_child;
            }
        }
        longest_path = max(longest_path, longest + second + 1);
        return longest + 1;
    }
};
```
