### 273. Integer to English Words (Hard)

https://leetcode.com/problems/integer-to-english-words/description/

```
class Solution {
public:
    string digit[20] = {"Zero", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten",
        "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"};
    string ten[10] = {"Zero", "Ten", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"};
    string numberToWords(int num) {
        if(num == 0) return "Zero";
        string res = intToString(num);
        return res.substr(1);
    }
    string intToString(int num) {
        if (num >= 1000000000) {
            return intToString(num / 1000000000) + " Billion" + intToString(num % 1000000000);
        } else if (num >= 1000000) {
            return intToString(num / 1000000) + " Million" + intToString(num % 1000000);
        } else if (num >= 1000) {
            return intToString(num / 1000) + " Thousand" + intToString(num % 1000);
        } else if (num >= 100) {
            return intToString(num / 100) + " Hundred" + intToString(num % 100);
        } else if (num >= 20) {
            return " " + ten[num / 10] + intToString(num % 10);
        } else if (num >= 1) {
            return " " + digit[num];
        } 
        return "";
    }
};
```
