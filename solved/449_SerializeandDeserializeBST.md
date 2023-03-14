### 449. Serialize and Deserialize BST (Medium)

https://leetcode.com/problems/serialize-and-deserialize-bst/

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
        if(root) {
            res += to_string(root->val) + " ";
            se(root->left, res);
            se(root->right, res);
        }
    }
    TreeNode* de(istringstream& in, int lower, int upper) {
        string val;
        auto it = in.tellg();
        in >> val;
        if (val.empty() || in.eof()) return NULL;
        const int num = stoi(val);
        if (num < lower || num > upper) {
            in.seekg(it);
            return NULL;
        }
        TreeNode* r = new TreeNode(num);
        r->left = de(in, lower, num);
        r->right = de(in, num, upper);
        return r;
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
        return de(in, INT_MIN, INT_MAX);
    }
};

// Your Codec object will be instantiated and called as such:
// Codec* ser = new Codec();
// Codec* deser = new Codec();
// string tree = ser->serialize(root);
// TreeNode* ans = deser->deserialize(tree);
// return ans;
```
