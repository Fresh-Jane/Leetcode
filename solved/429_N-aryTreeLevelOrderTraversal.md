### 429. N-ary Tree Level Order Traversal (Medium)

https://leetcode.com/problems/n-ary-tree-level-order-traversal/description/

```
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}

    Node(int _val) {
        val = _val;
    }

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
public:
    vector<vector<int>> levelOrder(Node* root) {
        if (!root) return {};
        vector<vector<int>> res;
        queue<Node*> q;
        q.push(root);
        while(!q.empty()) {
            int len = q.size();
            vector<int> level_res;
            while(len--) {
                Node* cur = q.front(); q.pop();
                level_res.push_back(cur->val);
                for (Node* c : cur->children) q.push(c);
            }
            res.push_back(level_res);
        }
        return res;
    }
};
```
