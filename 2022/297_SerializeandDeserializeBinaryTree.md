### 297. Serialize and Deserialize Binary Tree (Hard)

https://leetcode.com/problems/serialize-and-deserialize-binary-tree/

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
class Codec {
private:
    void se(TreeNode* root, string& res) {
        if (!root) {
            res += "# ";
            return;
        }
        res += to_string(root->val) + " ";
        se(root->left, res);
        se(root->right, res);
    }
    TreeNode* de(istringstream& in) {
        string val;
        in >> val;
        if (val == "#") return NULL;
        TreeNode* root = new TreeNode(stoi(val));
        root->left = de(in);
        root->right = de(in);
        return root;
    }
    
public:
    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        string res;
        se(root, res);
        return res;
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        istringstream in(data);
        return de(in);
    }
};

// Your Codec object will be instantiated and called as such:
// Codec ser, deser;
// TreeNode* ans = deser.deserialize(ser.serialize(root));
```
