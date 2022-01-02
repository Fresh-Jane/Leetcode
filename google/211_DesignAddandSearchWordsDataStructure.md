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
        for (const char c : word) {
            if (cur->next[c-'a'] == nullptr) 
                cur->next[c-'a'] = new Node();
            cur = cur->next[c-'a'];
        }
        cur->is_end = true;
    }
    
    bool search(string word) {
        return dfs(word, 0, root);
    }

private:
    struct Node {
        bool is_end = false;
        Node* next[26];
    };
    Node* root;
    bool dfs(const string& word, int i, Node* pre) {
        if (!pre) return false;
        if (i >= word.size()) return pre->is_end;
        const char c = word[i];
        if (c == '.') {
            for (int j = 0; j < 26; ++j)
                if (dfs(word, i+1, pre->next[j])) return true;
            return false;
        } else {
            return dfs(word, i+1, pre->next[c-'a']);
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
