---
title: 0168Excel表列名称

date: 2019-04-02

tags: [easy]


---

给定一个正整数，返回它在 Excel 表中相对应的列名称。

例如，

```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
    ...
```

**示例 1:**

```
输入: 1
输出: "A"
```

**示例 2:**

```
输入: 28
输出: "AB"
```

**示例 3:**

```
输入: 701
输出: "ZY"
```



建立一个字典

```python
class Solution:
    def convertToTitle(self, n):
        """
        :type n: int
        :rtype: str
        """
        from string import ascii_uppercase
        lst = []
        dct = dict(enumerate(ascii_uppercase, start=1))

        while n:
            n, mod = divmod(n, 26)
            if mod == 0:
                mod = 26
                n -= 1
            lst.append(mod)

        return ''.join([dct[i] for i in reversed(lst)])
```

```python
class Solution:
    def convertToTitle(self, n):
        """
        :type n: int
        :rtype: str
        """
        res = ''
        mod = n # in  case that n is 0 or less
        while True:
            if mod <= 0:
                break
            mod, remainder = divmod(mod, 26)
            if remainder == 0:
                mod -= 1
                res = 'Z' + res
            else:
                res = chr(64 + remainder) + res # ord(A) = 65
        return res
```

```python
class Solution:
    def convertToTitle(self, n):
        """
        :type n: int
        :rtype: str
        """
        res = ''
        while n :
            res = chr(ord('A') + (n - 1) % 26) + res
            n = (n - 1) // 26
        return res
```

