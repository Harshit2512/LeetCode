- **Time complexity** = O(n), n being the length of the list
- **Space complexity** = O(1)
- **Approach:** Using slow and fast pointers
    - Initialize two pointers: fast and slow both pointing to a **dummy node ahead of head**.
    - Move fast pointer n+1 steps forward to maintain a gap of n between slow and fast.
    - Move both fast and slow pointers **until fast pointer reaches the end**.
    - The **slow pointer will be at the node just before the target node**. Adjust its next pointer to skip the nth node from the end.
    - Return the head of the modified list.

```java

class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;

        ListNode slow = dummy;
        ListNode fast = dummy;

        // Move the fast point to create the gap between two points equivalent to gap b/w node to be removed and end of LL
        for (int i = 0; i <= n; i++ ) {
            fast = fast.next;
        }

        // Move both pointers until fast pointer reach to null, at this point slow pointer will reference to the node after which node to be removed
        while (fast != null) {
            slow = slow.next;
            fast = fast.next;
        }

        slow.next = slow.next.next;

        return dummy.next;
    }
}

```