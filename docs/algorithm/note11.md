# 环形链表
```java
public class LinkCycle {

    static class ListNode{
        int val;
        ListNode next;
        public ListNode(int val,ListNode next){
            this.val=val;
            this.next=next;
        }
    }

    public static void main(String[] args) {
        ListNode node5 = new ListNode(5,null);
        ListNode node4 = new ListNode(4,node5);
        ListNode node3 = new ListNode(3,node4);
        ListNode node2 = new ListNode(2,node3);
        ListNode node1 = new ListNode(1,node2);
        node5.next = node3;
        System.out.println(hasCycle(node1));
        System.out.println(hasCycle2(node1));
    }

    /**
     * 环形链表
     * 给定一个链表，判断链表中是否有环，如果链表中有某个节点，可以通过连续跟踪next指针再次到达该节点，则该链表中存在环。
     * 如果链表中存在环则返回true，否则返回false
     * @param head
     * @return
     */
    public static boolean hasCycle(ListNode head){
        // 迭代加打标记 该节点已经存在集合中则存在环
        Set<ListNode> set = new HashSet<>();
        while (head != null){
           if(!set.add(head)){
               return true;
           }
           head = head.next;
        }
        return false;
    }

    // 双指针 
    public static boolean hasCycle2(ListNode head){
       if(head == null || head.next == null){
           return false;
       }
       ListNode slow = head;
       ListNode quick = head.next;
       while (slow != quick){
           if(quick == null || quick.next == null){
               return false;
           }
           slow = head.next;
           quick = head.next.next;
       }
        return false;
    }
}
```