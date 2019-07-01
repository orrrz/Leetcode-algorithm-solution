# [136. Single Number](https://leetcode-cn.com/problems/single-number/)

### Description

Given a **non-empty** array of integers, every element appears *twice* except for one. Find that single one.

**Note:**

Your algorithm should have a linear runtime complexity(时间复杂度为 O(n) ). Could you implement it without using extra memory?（空间复杂度为 O(1) ）

**Example 1:**

```
Input: [2,2,1]
Output: 1
```

**Example 2:**

```
Input: [4,1,2,1,2]
Output: 4
```

<br>

### Solution 1

```java
// HashMap

class Solution {
    public int singleNumber(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<>();
        
        for (int num : nums) {
            if (map.containsKey(num)) 
                map.put(num, map.get(num) + 1);
            
            else
                map.put(num, 1);
        }
        
        for (Integer key : map.keySet()) {
            if (map.get(key) == 1) 
                return key;
        }
        return 0;

    }
}
```

<br>

### Solution 2

```java
// 考虑到算法应该具有线性时间复杂度，不使用额外空间实现，应该使用异或运算

// 1.相同的数异或为 0   n ^ n => 0
// 2.任何数与0异或为任何数  0 ^ n => n
// 交换律：a ^ b ^ c <=> a ^ c ^ b
// var a = [2,3,2,4,4]
// 2 ^ 3 ^ 2 ^ 4 ^ 4等价于 2 ^ 2 ^ 4 ^ 4 ^ 3 => 0 ^ 0 ^3 => 3

class Solution {
    public int singleNumber(int[] nums) {
        
        int result = nums[0];
        if (nums.length > 1) {
            for (int i = 1; i < nums.length; i ++) {
                result = result ^ nums[i];
            }
        }
        return result;
    }
}
```

<br>



# [137. Single Number II](https://leetcode-cn.com/problems/single-number-ii/)

### Description

Given a **non-empty** array of integers, every element appears *three* times except for one, which appears exactly once. Find that single one.

**Note:**

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

**Example 1:**

```
Input: [2,2,3,2]
Output: 3
```

**Example 2:**

```
Input: [0,1,0,1,0,1,99]
Output: 99
```

<br>

### Solution 1

```java
// HashMap

class Solution {
    public int singleNumber(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<>();
        
        for (int num : nums) {
            if (map.containsKey(num)) 
                map.put(num, map.get(num) + 1);
            
            else
                map.put(num, 1);
        }
        
        // Map 遍历的两种方式  
        // 1. public Set<K> keySet() keySet()得到集合中所有的键
        for (Integer key : map.keySet()) {
            if (map.get(key) == 1) 
                return key;
        }
        // 2. public Set<Map.Entry<K,V>> entrySet()得到所有键值对对象
        //for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
        //    if (entry.getValue() == 1) {
        //        return entry.getKey();
        //    }
        //}
        
        
        return 0;

    }
}
```

<br>



# [260. Single Number III](https://leetcode-cn.com/problems/single-number-iii/)

### Description

Given an array of numbers `nums`, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

**Example:**

```
Input:  [1,2,1,3,2,5]
Output: [3,5]
```

**Note**:

1. The order of the result is not important. So in the above example, `[5, 3]` is also correct.
2. Your algorithm should run in linear runtime complexity. Could you implement it using only constant space complexity?

<br>

### Solution 1

```java
// HashMap

class Solution {
    public int[] singleNumber (int[] nums) {
        
        int[] result = new int[2];
        HashMap<Integer, Integer> map = new HashMap<>();
        for (Integer num : nums) {
            if (map.containsKey(num)) 
                map.put(num, map.get(num) + 1);
            else
                map.put(num, 1);
        }
        
        int i = 0;
        for (Integer key : map.keySet()) {
            if (map.get(key) == 1) {
                result[i] = key;
                i ++;
            }
        }
        return result;
    }
}
```

<br>

### Solution 2

- 思路：位运算
  - 如果只有一个数据只出现一次的话，很简单的求亦或。
  - 两个的话自然有不同。但是我们可以知道的是，若a,b为所求，则前面累计的亦或值re = a^b，而re中为1的数位即是a和b中一个为1一个为0的。
  - 我们随机取一位，那么所有数据可以分成两组。一组该位为1，另一组为0，而a和b分别在这两组中。同样地，我们可以看到，除了a和b之外，每组其他的数据都出现2次。这样我们就转化成了上述的简单求亦或。
  - 因而问题变成，**取得re中某为1的数位，将数据分成两组**。

```python
class Solution(object):
      def singleNumber(self, nums):
          re = 0
          for num in nums:
              re ^= num

          n = re & (~(re - 1)) #取为1的最低位
          a = 0
          b = 0
          for num in nums:
              if n & num:  #将数据按该为是否为1分成两组
                  a ^= num
              else:
                  b ^= num
          return a, b
```





### Note

异或运算：两个相同的元素异或运算之后结果为 0

​		  任何数与 0 进行异或运算，结果都为其本身