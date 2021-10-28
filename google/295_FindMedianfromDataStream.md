### 295. Find Median from Data Stream (Hard)

https://leetcode.com/problems/find-median-from-data-stream/

https://leetcode.com/problems/find-median-from-data-stream/discuss/74062/Short-simple-JavaC%2B%2BPython-O(log-n)-%2B-O(1)

```
// Use 2 priority queue (max heap), small save half smaller ones and large for the half larger ones.
class MedianFinder {
public:
    void addNum(int num) {
        small.push(num);
        large.push(-small.top());
        small.pop();
        while(small.size() < large.size()) {
            small.push(-large.top());
            large.pop();
        }
    }
    
    double findMedian() {
        return small.size() > large.size() ? small.top() : (small.top() - large.top()) / 2.0;
    }
private:
    priority_queue<int> small, large; 
};

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder* obj = new MedianFinder();
 * obj->addNum(num);
 * double param_2 = obj->findMedian();
 */
```
