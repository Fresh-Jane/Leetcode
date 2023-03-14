### 588. Design In-Memory File System (Hard)

https://leetcode.com/problems/design-in-memory-file-system/

```
// Use two unordered_map
class FileSystem {
public:
    FileSystem() {
        ptree["/"] = {};
    }
    
    vector<string> ls(string path) {
        sort(ptree[path].begin(), ptree[path].end());
        return ptree[path];
    }
    
    void mkdir(string path, bool is_dir = true) {
        for (int i = 0; i < path.size(); ++i) if (path[i] == '/') path[i] = ' ';
        istringstream in(path);
        string each_f, pre, cur;
        while(in >> each_f) {
            cur = pre + "/" + each_f;
            if (!ptree.count(cur)) {
                if (pre.empty()) pre = "/";
                ptree[pre].push_back(each_f);
                ptree[cur] = {};
            }
            pre = cur;
        }
        if (!is_dir) ptree[cur].push_back(each_f);
    }
    
    void addContentToFile(string filePath, string content) {
        if (!ctree.count(filePath)) mkdir(filePath, false);
        ctree[filePath] += content;
    }
    
    string readContentFromFile(string filePath) {
        return ctree[filePath];
    }
private:
    unordered_map<string, vector<string>> ptree;
    unordered_map<string, string> ctree;
};

// Use Node struct
class FileSystem {
public:
    struct Node {
        bool is_dir;
        string content;
        unordered_map<string, Node*> children;
    };
    Node* root;

    FileSystem() {
        root = new Node();
        root->is_dir = true;
    }

    vector<string> ls(string path) {
        istringstream in(path);
        string token;
        Node* node = root;
        while (getline(in, token, '/')) {
            if (token.empty()) continue;
            node = node->children[token];
        }
        if (node->is_dir) {
            vector<string> res;
            for (const auto& p : node->children) res.push_back(p.first);
            sort(res.begin(), res.end());
            return res;
        } else {
            return {token};
        }
    }

    void mkdir(string path) {
        istringstream in(path);
        string token;
        Node* node = root;
        while (getline(in, token, '/')) {
            if (token.empty()) continue;
            if (!node->children.count(token)) {
                Node* c = new Node();
                c->is_dir = true;
                node->children[token] = c;
            }
            node = node->children[token];
        }
    }

    void addContentToFile(string filePath, string content) {
        istringstream in(filePath);
        string token;
        Node* node = root;
        while (getline(in, token, '/')) {
            if (token.empty()) continue;
            if (!node->children.count(token)) {
                Node* c = new Node();
                c->is_dir = false;
                node->children[token] = c;
            }
            node = node->children[token];
        }
        node->content += content;
    }

    string readContentFromFile(string filePath) {
        istringstream in(filePath);
        string token;
        Node* node = root;
        while (getline(in, token, '/')) {
            if (token.empty()) continue;
            node = node->children[token];
        }
        return node->content;
    }
};

/**
 * Your FileSystem object will be instantiated and called as such:
 * FileSystem* obj = new FileSystem();
 * vector<string> param_1 = obj->ls(path);
 * obj->mkdir(path);
 * obj->addContentToFile(filePath,content);
 * string param_4 = obj->readContentFromFile(filePath);
 */
```
