### 1352. Product of the Last K Numbers (Medium)

https://leetcode.com/problems/product-of-the-last-k-numbers/

```
// All product before 0 will be 0, so just save the prefix product after 0.
class ProductOfNumbers {
public:
    ProductOfNumbers() {
        AllPro = {1};
    }
    
    void add(int num) {
        if (num) AllPro.push_back(AllPro.back() * num);
        else AllPro = {1};
    }
    
    int getProduct(int k) {
        return k < AllPro.size() ? AllPro.back() / AllPro[AllPro.size()-k-1] : 0;
    }
private:
    vector<int> AllPro;
};

/**
 * Your ProductOfNumbers object will be instantiated and called as such:
 * ProductOfNumbers* obj = new ProductOfNumbers();
 * obj->add(num);
 * int param_2 = obj->getProduct(k);
 */
```
