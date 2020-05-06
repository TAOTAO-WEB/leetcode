## [合并K个排序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/)

合并 k 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

**示例:**

```
输入:
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6
```

分治思想

```java
public ListNode mergeKLists(ListNode[] lists) {
        if(lists.length == 0) return null;
        if(lists.length == 1) return lists[0];
        if(lists.length == 2) return mergetwolist(lists[0],lists[1]);

        int mid = lists.length/2;
        ListNode[] l1 = new ListNode[mid];
        ListNode[] l2 = new ListNode[lists.length-mid];
        for (int i=0;i<mid;i++){
            l1[i] = lists[i];
        }
        for (int i=mid,j=0;i<lists.length;i++,j++){
            l2[j] = lists[i];
        }
        return mergetwolist(mergeKLists(l1),mergeKLists(l2));
    }

    private ListNode mergetwolist(ListNode l1,ListNode l2){
        if(l1==null) return l2;
        if(l2==null) return l1;

        ListNode head=null;
        if(l1.val>l2.val){
            head=l2;
            head.next = mergetwolist(l1,l2.next);
        }
        else {
            head=l1;
            head.next = mergetwolist(l1.next,l2);
        }
        return head;
    }
```

