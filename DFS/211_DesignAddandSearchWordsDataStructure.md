### 211. Design Add and Search Words Data Structure (Medium)

https://leetcode.com/problems/design-add-and-search-words-data-structure/

```
class WordDictionary {
public:
    WordDictionary() {
        root = new Node();
    }
    
    void addWord(string word) {
        Node* cur = root;
        for (char c : word) {
            if (cur->next[c-'a'] == NULL)
                cur->next[c-'a'] = new Node();
            cur = cur->next[c-'a'];
        }
        cur->is_end = true;
    }
    
    bool search(string word) {
        return dfs(word, 0, root);
    }
private:
    struct Node{
        bool is_end;
        Node* next[26];
    };
    Node* root;
    // We must transfer quote as parameter and use string will be TLE.
    bool dfs(const string& w, int len, Node* root) {
        if (!root) return false;
        if (len == w.size()) return root->is_end;
        char c = w[len];
        if (c == '.') {
            for (int i = 0; i < 26; ++i) 
                if (dfs(w, len+1, root->next[i])) return true;
            return false;
        } else {
            return dfs(w, len+1, root->next[c-'a']);
        }
    }
};

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary* obj = new WordDictionary();
 * obj->addWord(word);
 * bool param_2 = obj->search(word);
 */
```
