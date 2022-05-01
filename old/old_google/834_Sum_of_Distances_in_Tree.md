### 834. Sum of Distances in Tree (Hard)

An undirected, connected tree with N nodes labelled 0...N-1 and N-1 edges are given.

The ith edge connects nodes edges[i][0] and edges[i][1] together.

Return a list ans, where ans[i] is the sum of the distances between node i and all other nodes.

Example 1:

```
Input: N = 6, edges = [[0,1],[0,2],[2,3],[2,4],[2,5]]
Output: [8,12,6,10,10,10]
Explanation: 
Here is a diagram of the given tree:
  0
 / \
1   2
   /|\
  3 4 5
We can see that dist(0,1) + dist(0,2) + dist(0,3) + dist(0,4) + dist(0,5)
equals 1 + 1 + 2 + 2 + 2 = 8.  Hence, answer[0] = 8, and so on.
```

Note: 1 <= N <= 10000

```
// https://leetcode.com/problems/sum-of-distances-in-tree/discuss/130583/C%2B%2BJavaPython-Pre-order-and-Post-order-DFS-O(N)
class Solution {
public:
    vector<unordered_set<int>> tree;
    vector<int> res, count;
    vector<int> sumOfDistancesInTree(int N, vector<vector<int>>& edges) {
        tree.resize(N);
        res.assign(N, 0);
        count.assign(N, 1);
        for (auto e : edges) {
            tree[e[0]].insert(e[1]);
            tree[e[1]].insert(e[0]);
        }
        post_dfs(0, -1);
        pre_dfs(0, -1);
        return res;
    }
    void post_dfs(int root, int pre) {
        for (int i : tree[root]) {
            if (i == pre) continue;
            post_dfs(i, root);
            count[root] += count[i];
            res[root] += res[i] + count[i];
        }
    }
    void pre_dfs(int root, int pre) {
        for (int i : tree[root]) {
            if (i == pre) continue;
            res[i] = res[root] - count[i] + count.size() - count[i];
            pre_dfs(i, root);
        }
    }
};
```

