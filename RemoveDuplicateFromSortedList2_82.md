- **Time complexity** = O(n), need to traverse all nodes in the list once
- **Space complexity** = O(1)
- **Approach:** Two Pointers with Dummy Node
    - Two pointers (prev and currentNode). Intially point prev to dummy node and head to currentNode
    - Keep running while loop until currentNode.val equals currentNode.next.val
    - Check if prev.next is same as currentNode. If so then there is no duplicate in between. If not same then (duplicate), point prev.next to currentNode.next (removes all duplicates)

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
    public ListNode deleteDuplicates(ListNode head) {

        // Time complexity = O(n), need to traverse all nodes in the list once
        // Space complexity = O(1)
        // https://github.com/AlgoMaster-io/leetcode-solutions/blob/main/java/remove-duplicates-from-sorted-list-ii.md

        // dummy node is required to handle edge case where there is no node or duplicate starts from beginning (ex - 2)
        ListNode dummy = new ListNode(-101);

        // prev node is the pointer to know start of the duplication
        ListNode prev = dummy;

        dummy.next = head;
        ListNode currentNode = head;

        while (currentNode != null) {
            while (currentNode.next != null && currentNode.val == currentNode.next.val) {
                currentNode = currentNode.next;                
            }

            // if node next to prev is the current node, means both are found consecutive and there is no duplicate/s in between
            if (prev.next == currentNode) {
                prev = prev.next;
            } else {
                prev.next = currentNode.next;                
            }
            currentNode = currentNode.next;
        }
        return dummy.next;       
    }
}

```