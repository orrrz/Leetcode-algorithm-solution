# [771. Jewels and Stones](https://leetcode-cn.com/problems/jewels-and-stones/)

### Description

You're given strings `J` representing the types of stones that are jewels, and `S` representing the stones you have.  Each character in `S` is a type of stone you have.  You want to know how many of the stones you have are also jewels.

The letters in `J` are guaranteed distinct, and all characters in `J` and `S` are letters. Letters are case sensitive, so `"a"` is considered a different type of stone from `"A"`.

**Example 1:**

```
Input: J = "aA", S = "aAAbbbb"
Output: 3
```

**Example 2:**

```
Input: J = "z", S = "ZZ"
Output: 0
```

**Note:**

- `S` and `J` will consist of letters and have length at most 50.
- The characters in `J` are distinct.

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