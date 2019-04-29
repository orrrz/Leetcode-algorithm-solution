# [7. Reverse Integer](https://leetcode-cn.com/problems/reverse-integer/)

### Description

Given a 32-bit signed integer, reverse digits of an integer.

**Example 1:**

```
Input: 123
Output: 321
```

**Example 2:**

```
Input: -123
Output: -321
```

**Example 3:**

```
Input: 120
Output: 21
```

**Note:**
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

<br>

### Solution1

```java
class Solution {
    public int reverse(int x) {
        try {
            StringBuilder sb = new StringBuilder();
            sb.append(x);
            if (x >= 0) {
                sb.reverse();
            }else {
                sb.deleteCharAt(0);
                sb.reverse();
                sb.insert(0, "-");
            }
            return Integer.parseInt(sb.toString());
        }catch(Exception e) {
            return 0;
        }
    }
}
```



<br>

### Note

- Solution1
  - 如果传入参数为负数，需要删除，反转，插入。
  - StringBuilder.delete（int start, int end），删除索引从start（包含start）到end（不包含end）的所有字符；
  - StringBuilder.deleteCharAt（int index）方法，删除指定索引的字符
  - `Integer.parseInt(sb.toString())`，此方法会将字符串前多余的0去除。
