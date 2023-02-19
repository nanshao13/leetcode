#### [28. 找出字符串中第一个匹配项的下标](https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string/)

KMP算法一般有三种next数组，这里只会一种，以-1、0开头。

```cpp
class Solution {
public:
    void getNext(int* next, const string& needle, int nSize) {
        next[0] = -1;
        int k = -1;
        int i = 1;
        while (i < nSize) {
            if (k == -1 || needle[k] == needle[i - 1]) {
                next[i] = k + 1;
                ++k;
                ++i;
            } else {
                k = next[k];
            }
        }
    }
    int strStr(string haystack, string needle) {
        int hSize = haystack.size();
        int nSize = needle.size();
        if (hSize < nSize) {
            return -1;
        }
        int next[nSize];
        getNext(next, needle, nSize);
        int i = 0;
        int j = 0;
        while (i < hSize && j < nSize) {
            if (j == -1 || haystack[i] == needle[j]) {
                ++i;
                ++j;
            } else {
                j = next[j];
            }
        }
        if (j >= nSize) {
            return i - j;
        }
        return -1;
    }
};
```

tips：由于这种KMP算法的next的开头是-1、0开始的，那么j就可能回溯到-1，而此时再跟needle.size()比较就会出错，因为像这种调用类方法取得的size都是无符号整数，负数和无符号整数比较大小时，负数会提升为无符号整数，而无符号整数的-1是2^32-1。
