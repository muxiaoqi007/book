实现 [strStr()](https://baike.baidu.com/item/strstr/811469) 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  **-1**。

**示例 1:**

```
输入: haystack = "hello", needle = "ll"
输出: 2
```

**示例 2:**

```
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```

**说明:**

当 `needle` 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 `needle` 是空字符串时我们应当返回 0 。这与C语言的 [strstr()](https://baike.baidu.com/item/strstr/811469) 以及 Java的 [indexOf()](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)) 定义相符。

强大的find

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        return haystack.find(needle)
```

```c++
class Solution {
public:
    int strStr(string haystack, string needle) {
        return haystack.find(needle);
    }
};

```

直接返回index

```python
class Solution:
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        try:
            index = haystack.index(needle)
            return index
        except:
            return -1
```

split

```python
class Solution:
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        if haystack and needle and needle in haystack:
            res = haystack.split(needle)
            return len(res[0])
        if not needle:
            return 0
        return -1
```

KMP

```python
class Solution(object):
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """ 
        text, pattern = haystack, needle
        if not pattern or len(pattern) == 0:
            return 0
        
        lps = self.findLPS(pattern) # longest proper prefix which is also suffix
        i, j = 0, 0 # idx for text and pattern
        res = -1
        while i < len(text):
            if pattern[j] == text[i]:
                i += 1
                j += 1
            if j == len(pattern):
                res = i - j
                return res
                j = lps[j-1]
            elif i < len(text) and pattern[j] != text[i]: # mismatch after j matches 
                if j != 0: # Don't match lps[0..lps[j-1]] characters, they will match anyway 
                    j = lps[j-1]
                else:
                    i += 1  
        return res

    def findLPS(self, pattern): 
        length, lps = 0, [0]
        for i in range(1, len(pattern)):
            while length > 0 and pattern[length] != pattern[i]:
                length = lps[length-1]
            if pattern[length] == pattern[i]:
                length += 1
            lps.append(length)
        return lps
```



```c++
class Solution {
public:
    int strStr(string haystack, string needle) {
        int n = haystack.length(), m = needle.length();
        if (m == 0)
            return 0;
        vector<int> next(m);
        next[0] = -1;
        int j = -1;
        for (int i = 1; i < m; i++) {
            while (j > -1 && needle[i] != needle[j + 1]) j = next[j];
            if (needle[i] == needle[j + 1]) j++;
            next[i] = j;
        }
        j = -1;
        for (int i = 0; i < n; i++) {
            while (j > -1 && haystack[i] != needle[j + 1]) j = next[j];
            if (haystack[i] == needle[j + 1]) j++;
            if (j == m - 1)
                return i - m + 1;
        }
        return -1;
    }
};

```

