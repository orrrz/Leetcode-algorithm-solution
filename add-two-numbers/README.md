# [2  Add Two Numbers](https://leetcode-cn.com/problems/add-two-numbers/)

### Description

>给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。
>
>如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。
>
>您可以假设除了数字 0 之外，这两个数都不会以 0 开头。
>
>示例：
>
>输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
>输出：7 -> 0 -> 8
>原因：342 + 465 = 807

### Solution1(Official)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode dummyHead = new ListNode(0);	// 初始化一个哑节点作为返回值
    ListNode p = l1, q = l2, curr = dummyHead;
    int carry = 0;	// 进位，两树相加最大进位只可能是0,1（9+9+1 = 19）
    while (p != null || q != null) {
        int x = (p != null) ? p.val : 0;	// 假设p==null,即到达链表的末尾，则设置其值为0
        int y = (q != null) ? q.val : 0;
        int sum = carry + x + y;
        carry = sum / 10;	// 更新进位
        curr.next = new ListNode(sum % 10);	// 创建一个新节点储存（sum%10），设置为当前节点的下一个节点
        curr = curr.next;	// 前进
        if (p != null) p = p.next;
        if (q != null) q = q.next;
    }
    // 检查进位是否大于1，如果是，向返回列表追加一个新节点为1
    if (carry > 0) {
        curr.next = new ListNode(carry);
    }
    return dummyHead.next;	// 返回dummyHead的下一个节点
}
```



### Solution2

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        return subFunc(l1, l2, 0);
    }
    
    public ListNode subFunc(ListNode l1, ListNode l2, int carry) {
        int sum = l1.val + l2.val + carry;
        ListNode node = new ListNode(sum % 10);
        carry = sum / 10;
        if (l1.next == null && l2.next == null) {
            if (carry != 0) {
                node.next = new ListNode(carry);
            }
            // node.next = subFunc(l1.next, l2.next, m);
        }else if (l1.next == null) {
            node.next = subFunc(new ListNode(0), l2.next, carry);
        }else if (l2.next == null) {
            node.next = subFunc(l1.next, new ListNode(0), carry);
        }else if(l1.next != null && l2.next != null){
            node.next = subFunc(l1.next, l2.next, carry);
        }
        return node;
        
    } 
}   
```

### Note

- Solution1注意点
  - 维护一个dummyHead用于简化代码
  - 进位只可能为0,1
  - 判断节点是否为空，如果是，设置节点值为0
  - 两个节点进入下一位之前，需要判断节点是否为空，不为空才可以前进
  - 循环完整个链表后，还需要判断进位是否为1，如果是，需要向返回列表追加一个含有数字1的新节点
