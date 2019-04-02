#### [709. To Lower Case](https://leetcode-cn.com/problems/to-lower-case/)

### Description

Implement function ToLowerCase() that has a string parameter str, and returns the same string in lowercase.

实现函数 ToLowerCase()，该函数接收一个字符串参数 str，并将该字符串中的大写字母转换成小写字母，之后返回新的字符串。

### Solution

```java
大小 --> 小写
chars[i] += 'a' - 'A';
小写 --> 大写
chars[i] += 'A' - 'a';
```

### Note

- 大小写替换的算式

