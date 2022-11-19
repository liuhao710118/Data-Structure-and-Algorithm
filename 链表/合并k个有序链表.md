题目链接：[23. 合并K个升序链表 - 力扣（LeetCode）](https://leetcode.cn/problems/merge-k-sorted-lists/comments/)

困难程度：hard

代码实现：

```java
public ListNode mergeKLists(ListNode[] lists) {
        ListNode head = null;
        ListNode header = null;
        PriorityQueue<ListNode> pq = new PriorityQueue<>((e1, e2) -> e1.val == e2.val ? 0 : e1.val > e2.val ? 1 : -1);
        for (ListNode node : lists) {
            if(node != null){
                pq.add(node);
            }
        }
        while (!pq.isEmpty()) {
            ListNode peek = pq.poll();
            if (head == null) {
                head = new ListNode();
                head.val = peek.val;
                header = head;
            } else {
                head.next = new ListNode();
                head.next.val = peek.val;
                head = head.next;
            }
            if (peek.next != null) {
                pq.offer(peek.next);
            }
        }
        return header;
    }
```



> 合并 `k` 个有序链表的逻辑类似合并两个有序链表，难点在于，如何快速得到 `k` 个节点中的最小节点，接到结果链表上？
>
> 这里我们就要用到 [优先级队列（二叉堆）](https://labuladong.gitee.io/algo/2/23/65/) 这种数据结构，把链表节点放入一个最小堆，就可以每次获得 `k` 个节点中的最小节点  ----来着labuladong的算法小抄



![image-20221119180535276](resources/%E5%90%88%E5%B9%B6k%E4%B8%AA%E6%9C%89%E5%BA%8F%E9%93%BE%E8%A1%A8.assets/image-20221119180535276.png)