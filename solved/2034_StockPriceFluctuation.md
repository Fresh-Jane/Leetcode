### 2034. Stock Price Fluctuation (Medium)

https://leetcode.com/problems/stock-price-fluctuation/

```
class StockPrice {
public:
    StockPrice() {}
    
    void update(int timestamp, int price) {
        if (m.find(timestamp) != m.end()) 
            cnt.erase(cnt.find(m[timestamp]));
        m[timestamp] = price;
        cnt.insert(price);
    }
    
    int current() {
        return m.rbegin()->second;
    }
    
    int maximum() {
        return *cnt.rbegin();
    }
    
    int minimum() {
        return *cnt.begin();
    }
private:
    map<int, int> m;
    multiset<int> cnt;
};

/**
 * Your StockPrice object will be instantiated and called as such:
 * StockPrice* obj = new StockPrice();
 * obj->update(timestamp,price);
 * int param_2 = obj->current();
 * int param_3 = obj->maximum();
 * int param_4 = obj->minimum();
 */
```
