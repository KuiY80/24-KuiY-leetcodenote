#     	[剑指 Offer 22]链表中倒数第k个节点	80.1%	Easy	0.0%
我的思路：双指针
```
class Solution {
    public ListNode getKthFromEnd(ListNode head, int k) {
        ListNode former=head,latter =head;
        for (int i=0;i<k;i++){
            former=former.next;
        }
        while(former !=null){
            former=former.next;
            latter=latter.next;
        }
        return  latter;

    }
}
```

#    	[剑指 Offer 24]反转链表	74.2%	Easy	0.0%

我的思路：双链表
```
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev=null;
        ListNode curr=head;
        while ( curr!=null){
            ListNode next=curr.next; // 暂存后继节点
            curr.next=prev; // 修改引用指向
            prev =curr;// 暂存当前节点 移动
            curr =next;  // 访问下一节点
        }
        return prev;

    }
}

```
#     	[剑指 Offer 25]合并两个排序的链表	72.3%	Easy	0.0%
题解思路：伪节点
根据题目描述，     算法流程：
    1.初始化： 伪头节点 dum ，节点 cur 指向 dum 。
    2.循环合并： 当 l1或 l2为空时跳出；
    当 l1.val<l2.val 时： cur 的后继节点指定为 l1，并 l1向前走一步；
    当 l1.val≥l2.val 时： cur 的后继节点指定为 l2，并 l2向前走一步 ；
    节点 cur 向前走一步，即 cur=cur.next 。
    3.合并剩余尾部： 跳出时有两种情况，即 l1为空 或 l2为空。
    若 l1不等于null ： 将 l1添加至节点 cur 之后；
    否则： 将 l2添加至节点 cur 之后。
    4.返回值： 合并链表在伪头节点 dum 之后，因此返回 dum.next 即可。

    ```
    class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dum =new ListNode(0),cur =dum;
        while(l1 !=null && l2 != null){
            if (l1.val <l2.val){
                cur.next =l1;
                l1= l1.next;
            }else{
                cur.next =l2;
                l2 =l2.next;
            }
            cur =cur.next;
        }
        cur.next =l1 !=null ? l1 :l2;
        return dum.next;

    }
}
    ```