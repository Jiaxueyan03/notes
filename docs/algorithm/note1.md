
例如：输入 1->2->3->4->5
    输出：5->4->3->2->1

方法一：迭代方式实现
```java
static class ListNode {
        int val;
        ListNode next;

        public ListNode(int val,ListNode next){
            this.val = val;
            this.next = next;
        }


    }

    public static void main(String[] args) {
        ListNode node5 = new ListNode(5,null);
        ListNode node4 = new ListNode(4,node5);
        ListNode node3 = new ListNode(3,node4);
        ListNode node2 = new ListNode(2,node3);
        ListNode node1 = new ListNode(1,node2);
        ListNode node = iterate(node1);
        System.out.println(node);
    }


    public static ListNode iterate(ListNode head){
        ListNode prev = null , next;
        ListNode curr = head;
        while (null != curr){
            next = curr.next;
            curr.next = prev;
             prev = curr;
             curr = next;
        }
        return prev;
    }
}
```

方法二：递归实现


```java
 public static ListNode recursion(ListNode head){
        if(null == head || null == head.next){
            return head;
        }
        ListNode newHead = recursion(head.next);
        head.next.next = head;
        head.next=null;
        return newHead;
    }

```
