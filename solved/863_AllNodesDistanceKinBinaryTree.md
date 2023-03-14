### 863. All Nodes Distance K in Binary Tree (Medium)

https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
// First dfs to link nodes and their parent.
// Next BFS to get all k distance results from the target node.
class Solution {
public:
    unordered_map<TreeNode*, TreeNode*> parent;  // node -> parent
    void dfs(TreeNode* root, TreeNode* p) {
        if (!root) return;
        parent[root] = p;
        dfs(root->left, root);
        dfs(root->right, root);
    }
    vector<int> distanceK(TreeNode* root, TreeNode* target, int k) {
        dfs(root, NULL);
        unordered_map<TreeNode*, bool> visit;
        queue<TreeNode*> q;
        q.push(target);
        visit[target] = true;
        int dis = 0;
        vector<int> res;
        while(!q.empty()) {
            if (dis++ == k) break;
            int len = q.size();
            while(len--) {
                TreeNode* cur = q.front(); q.pop();
                if (cur->left && !visit.count(cur->left)) {
                    q.push(cur->left);
                    visit[cur->left] = true;
                }
                if (cur->right && !visit.count(cur->right)) {
                    q.push(cur->right);
                    visit[cur->right] = true;
                }
                if (parent[cur] && !visit.count(parent[cur])) {
                    q.push(parent[cur]);
                    visit[parent[cur]] = true;
                }
            }
        }
        while(!q.empty()) {
            res.push_back(q.front()->val); q.pop();
        }
        return res;
    }
};

// First find the path from root to the target and record the distance of each nodes on the path.
// Second dfs the tree and add the nodes with the k distance to the target.
// https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/discuss/143798/1ms-beat-100-simple-Java-dfs-with(without)-hashmap-including-explanation
class Solution {
public:
    unordered_map<TreeNode*, int> dist;
    vector<int> res;
    vector<int> distanceK(TreeNode* root, TreeNode* target, int k) {
        if (!root) return res;
        find(root, target);
        dfs(root, dist[root], k);
        return res;
    }
    int find(TreeNode* root, TreeNode* target) {
        if (!root) return -1;
        if (root == target) {
            dist[root] = 0;
            return 0;
        }
        int left = find(root->left, target);
        if (left >= 0) {
            dist[root] = left+1;
            return left+1;
        }
        int right = find(root->right, target);
        if (right >= 0) {
            dist[root] = right+1;
            return right+1;
        }
        return -1;
    }
    void dfs(TreeNode* root, int len, int k) {
        if (!root) return;
        if (dist.count(root)) len = dist[root];
        if (len == k) res.push_back(root->val);
        dfs(root->left, len+1, k);
        dfs(root->right, len+1, k);
    }
};
```
