### 355. Design Twitter (Medium)

https://leetcode.com/problems/design-twitter/description/

```
class Twitter {
private:
    unordered_map<int, unordered_set<int>> follows;
    unordered_map<int, vector<pair<int, int>>> posts;
    int timestamp;

    using vpit = vector<pair<int, int>>::iterator;
    struct Cmp {
        bool operator() (const pair<vpit, vpit>& p1, const pair<vpit, vpit>& p2) {
            return p1.first->first < p2.first->first;
        }
    };

public:
    Twitter() {
        timestamp = 0;
    }
    
    void postTweet(int userId, int tweetId) {
        posts[userId].push_back({timestamp++, tweetId});
    }
    
    vector<int> getNewsFeed(int userId) {
        vector<int> res;
        priority_queue<pair<vpit, vpit>, vector<pair<vpit, vpit>>, Cmp> pq;
        if (posts.count(userId) && !posts[userId].empty()) pq.push({--posts[userId].end(), posts[userId].begin()});
        if (follows.count(userId)) 
            for (int follow : follows[userId]) 
                if (posts.count(follow) && !posts[follow].empty()) pq.push({--posts[follow].end(), posts[follow].begin()});

        while(!pq.empty() && res.size() < 10) {
            auto cur = pq.top(); pq.pop();
            res.push_back(cur.first->second);
            if (--cur.first >= cur.second) pq.push(cur);
        }    
        return res;
    }
    
    void follow(int followerId, int followeeId) {
        if (followerId == followeeId) return;
        follows[followerId].insert(followeeId);
    }
    
    void unfollow(int followerId, int followeeId) {
        follows[followerId].erase(followeeId);
    }
};

/**
 * Your Twitter object will be instantiated and called as such:
 * Twitter* obj = new Twitter();
 * obj->postTweet(userId,tweetId);
 * vector<int> param_2 = obj->getNewsFeed(userId);
 * obj->follow(followerId,followeeId);
 * obj->unfollow(followerId,followeeId);
 */
```
