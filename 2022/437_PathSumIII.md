### 437. Path Sum III (Medium)

https://leetcode.com/problems/path-sum-iii/

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
// DFS
// hashmap m records the occur times of sum from root to current nodes.
// And m[sum-target] can get the number of path end with the current node and sum is target.
// Time: O(n) 
class Solution {
public:
    int res = 0;
    unordered_map<int, int> m;
    int pathSum(TreeNode* root, int targetSum) {
        m[0] = 1;
        dfs(root, 0, targetSum);
        return res;
    }
    void dfs(TreeNode* root, long long sum, int targetSum) {
        if (!root) return;
        sum += root->val;
        res += m[sum - targetSum];
        
        m[sum]++;
        dfs(root->left, sum, targetSum);
        dfs(root->right, sum, targetSum);
        m[sum]--;
    }
};

// Transfer all path sum vector from root to the curent node as one function parameter.
// Time: O(nlogn)
class Solution {
public:
    int res;
    int pathSum(TreeNode* root, int targetSum) {
        res = 0;
        vector<long long> path;
        dfs(root, path, targetSum);
        return res;
    }
    void dfs(TreeNode* root, vector<long long> path, int tar) {
        if (!root) return;
        if (root->val == tar) res++;
        for (int i = 0; i < path.size(); ++i) {
            path[i] += root->val;
            if (path[i] == tar) res++;
        }
        path.push_back(root->val);
        dfs(root->left, path, tar);
        dfs(root->right, path, tar);
    }
};
```
