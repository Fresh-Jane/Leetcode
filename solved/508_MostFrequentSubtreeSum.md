### 508. Most Frequent Subtree Sum (Medium)

https://leetcode.com/problems/most-frequent-subtree-sum/description/

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
class Solution {
public:
    int getSum(TreeNode* root, int& fre, unordered_map<int, int>& sum_m) {
        if (!root) return 0;
        int res = root->val;
        res += getSum(root->left, fre, sum_m);
        res += getSum(root->right, fre, sum_m);
        fre = max(fre, ++sum_m[res]);
        return res;
    }
    vector<int> findFrequentTreeSum(TreeNode* root) {
        if (!root) return {};
        unordered_map<int, int> sum_m;
        int fre = 0;
        getSum(root, fre, sum_m);
        vector<int> res;
        for (const auto& pair : sum_m) if (pair.second == fre) res.push_back(pair.first);
        return res; 
    }
};
```
