### 133. Clone Graph (Medium)

https://leetcode.com/problems/clone-graph/

```
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> neighbors;
    Node() {
        val = 0;
        neighbors = vector<Node*>();
    }
    Node(int _val) {
        val = _val;
        neighbors = vector<Node*>();
    }
    Node(int _val, vector<Node*> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
};
*/

// DFS
class Solution {
public:
    Node* cloneGraph(Node* node) {
        if (!node) return nullptr;
        unordered_map<Node*, Node*> m;
        return dfs(node, m);
    }
    Node* dfs(Node* old_n, unordered_map<Node*, Node*>& m) {
        if (m.count(old_n)) return m[old_n];
        Node* new_n = new Node(old_n->val);
        m[old_n] = new_n;
        for (auto& f : old_n->neighbors) {
            new_n->neighbors.push_back(dfs(f, m));
        }
        return new_n;
    }
    
};
```
