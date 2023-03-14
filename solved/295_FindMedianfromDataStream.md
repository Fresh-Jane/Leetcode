### 295. Find Median from Data Stream (Hard)

https://leetcode.com/problems/find-median-from-data-stream/

```
First, let me double check if I have got the correct question.
The straighforward idea is we can store all number in the stream using vector. Once we add one new item, resort it and get the median results. 
The time complexity is O(1) for add and O(NlogN) for find. 
The next idea is that we can mantain a sorted list after each adding operation by inserting the new number into the suitable position.
We can use binary search to find this position and time complexity for add is O(N) as vector insert is O(N), binary search is O(logN) and find is O(1).
But actually, we don't need to mantain the whole sorted array, we only need the median one or two value.
We can use two heaps as one max_heap save the smaller half, one min_heap save the bigger half. 
```
```
class MedianFinder {
public:
    MedianFinder() {}
    
    void addNum(int num) {
        lo.push(num);
        hi.push(lo.top());
        lo.pop();
        if (hi.size() > lo.size()) {
            lo.push(hi.top());
            hi.pop();
        }
    }
    
    double findMedian() {
        return lo.size() > hi.size() ? lo.top() : ((double)(lo.top() + hi.top()) * 0.5); 
    }
private:
    priority_queue<int> lo; // max_heap
    priority_queue<int, vector<int>, greater<int>> hi; // min_heap
};

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder* obj = new MedianFinder();
 * obj->addNum(num);
 * double param_2 = obj->findMedian();
 */
```
