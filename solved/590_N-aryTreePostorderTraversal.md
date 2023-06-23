### 590. N-ary Tree Postorder Traversal (Easy)

https://leetcode.com/problems/n-ary-tree-postorder-traversal/description/

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
    vector<int> postorder(Node* root) {
        post(root);
        return res;
    }
    void post(Node* root) {
        if (!root) return;
        for (Node* c : root->children) post(c);
        res.push_back(root->val);
    }
};

// Iterative
// postorder: left-right-root is the reverse of preorder like root-right-left
class Solution {
public:
    vector<int> postorder(Node* root) {
        if (!root) return {};
        vector<int> res;
        stack<Node*> st;
        st.push(root);
        while(!st.empty()) {
            Node* cur = st.top(); st.pop();
            res.push_back(cur->val);
            for (int i = 0; i < cur->children.size(); ++i) st.push(cur->children[i]);
        }
        reverse(res.begin(), res.end());
        return res;
    }
};
```
