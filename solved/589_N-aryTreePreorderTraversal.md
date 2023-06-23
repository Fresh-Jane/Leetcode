### 589. N-ary Tree Preorder Traversal (Easy)

https://leetcode.com/problems/n-ary-tree-preorder-traversal/description/

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

// Recursive
class Solution {
public:
    vector<int> res;
    vector<int> preorder(Node* root) {
        pre(root);
        return res;
    }
    void pre(Node* root) {
        if (!root) return;
        res.push_back(root->val);
        for (Node* child : root->children) pre(child);
    }
};

// Iterative
class Solution {
public:  
    vector<int> preorder(Node* root) {
        if (!root) return {};
        vector<int> res;
        stack<Node*> st;
        st.push(root);
        while(!st.empty()) {
            Node* cur = st.top(); st.pop();
            res.push_back(cur->val);
            for (int i = cur->children.size() - 1; i >= 0; --i) st.push(cur->children[i]);
        }
        return res;
    }
};

```
