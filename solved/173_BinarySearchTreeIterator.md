### 173. Binary Search Tree Iterator (Medium)

https://leetcode.com/problems/binary-search-tree-iterator/

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
class BSTIterator {
public:
    BSTIterator(TreeNode* root) {
        cur = root;
    }
    
    bool hasNext() {
        return cur || !st.empty();
    }
    
    int next() {
        while(cur) {
            st.push(cur);
            cur = cur->left;
        }
        cur = st.top(); st.pop();
        int res = cur->val;
        cur = cur->right;
        return res;
    }
private:
    TreeNode* cur;
    stack<TreeNode*> st;
};

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator* obj = new BSTIterator(root);
 * int param_1 = obj->next();
 * bool param_2 = obj->hasNext();
 */
```
