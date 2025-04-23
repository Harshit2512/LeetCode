- **Time Complexity:** O(n log n), where n is the number of nodes in the linked list. Each split divides the list into two halves, and merging takes linear time.
- **Space Complexity:** O(log n) due to the recursive stack space.
- **Key Points:**
    - Recursively divide  LL into half from mid point and sort sub list
    - Keep merging sorted sublist on each recursive step

```java
class Solution {
    public ListNode sortList(ListNode head) {

        if (head == null || head.next == null) return head;

        ListNode slow = head;
        ListNode fast = head;
        ListNode prev = null;

        while (fast != null && fast.next != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        } 

        prev.next = null;

        ListNode leftHalf = sortList(head);
        ListNode rightHalf = sortList(slow);

        return mergeList(leftHalf, rightHalf);
        
    }

    ListNode mergeList(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;

        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                current.next = l1;
                l1 = l1.next;
            } else {
                current.next = l2;
                l2 = l2.next;
            }
            current = current.next;
        }

        current.next = l1 != null ? l1 : l2;
        return dummy.next;

    }
}
```