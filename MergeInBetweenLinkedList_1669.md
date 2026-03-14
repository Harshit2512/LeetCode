- **Time Complexity:** O(N), length of longest list
- **Space Complexity:** O(1), no additional space
- **Approach: linked list traversal**
    - While iterating list1, keep updating node to be detached from (based on a) and next node to connect to (based on b)
    - Connect list2 between detached list1 nodes

```java

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeInBetween(ListNode list1, int a, int b, ListNode list2) {
        int p = 0;
        ListNode curr = list1;
        ListNode start = null;
        ListNode next = null;
        System.out.println(curr.val);

        while (curr != null) {
            if (p == a) {
                start.next = null;
                p++;
                curr = curr.next;
            } else if (p > a && p <= b) {
                curr = curr.next;
                next = curr.next;
                p++;
            } else if (p > b) {
                next = curr;
                break;
            } else {
                start = curr;
                curr = curr.next;
                p++;
            }           
        }

        start.next = list2;
        ListNode curr2 = list2;
        ListNode prev = null;

        while (curr2 != null) {
            prev = curr2;
            curr2 = curr2.next;
        }

        prev.next = next;

        return list1;
    }
}

```