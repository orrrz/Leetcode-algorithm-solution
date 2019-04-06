# [771. Jewels and Stones](https://leetcode-cn.com/problems/jewels-and-stones/)

### Description

> 给定字符串J 代表石头中宝石的类型，和字符串 S代表你拥有的石头。 S 中每个字符代表了一种你拥有的石头的类型，你想知道你拥有的石头中有多少是宝石。
>
>J 中的字母不重复，J 和 S中的所有字符都是字母。字母区分大小写，因此"a"和"A"是不同类型的石头。
>
>示例 1:
>```
>输入: J = "aA", S = "aAAbbbb"
>输出: 3
>```
>示例 2:
>```
>输入: J = "z", S = "ZZ"
>输出: 0
>```
>注意:
>
>S 和 J 最多含有50个字母。
>J 中的字符不重复。

### Solution1:

```java
class Solution {
    public int numJewelsInStones(String J, String S) {
        int count = 0;
        char[] jChar = J.toCharArray();
        char[] sChar = S.toCharArray();
        Map<Character, Integer> map = new HashMap<Character, Integer>();
        for (int i = 0; i < jChar.length; i++) {
            map.put(jChar[i], i);
            
        }
        for (int j = 0; j < sChar.length; j++) {
                if (map.containsKey(sChar[j])) {
                    count ++;
                }
            }
        return count;
    }
}
```

### Solution2:

```java
class Solution {
    public int numJewelsInStones(String J, String S) {
    	int count = 0;
        for(char s : S.toCharArray()) {
            for (char j : J.toCharArray()) {
                if (j == s) {
                    count ++;
                    break;
                }
            }
        }
        return count;
    }
}
```

### Note

- Solution1
  - 使用HashMap去重，以及使用了Map.containsKey方法（判断Map集合对象中是否包含指定的键名）

- Solution2
  - 因为使用了break，所以J、S的循环先后顺序不能调换。
