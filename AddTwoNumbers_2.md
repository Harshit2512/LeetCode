- **Time complexity** = O(max(m, n)), where m and n are the lengths of the two lists. We iterate through both lists once.
- **Space complexity** = O(max(m, n)). The result can be at most max(m, n) + 1 in length to accommodate any carry.
- Key Points: 
    - Create dummy head
    - How to calculate the sum (pVal + qVal + carry) , carry(sum / 10) and creat new node (sum % 10)

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

public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode dummyHead = new ListNode(0); // Dummy node to form the result list
    ListNode p = l1, q = l2, current = dummyHead; // Pointers for list traversal
    int carry = 0; // Initialize carry to zero
    
    while (p != null || q != null) {
        // Get the current values from the list nodes or use 0 if node is null
        int x = (p != null) ? p.val : 0;
        int y = (q != null) ? q.val : 0;
        
        int sum = carry + x + y; // Sum current digits and carry
        carry = sum / 10; // Update carry for next iteration
        
        current.next = new ListNode(sum % 10); // Create node for the digit sum
        current = current.next; // Move to the next node in result
        
        // Advance p and q pointers
        if (p != null) p = p.next;
        if (q != null) q = q.next;
    }
    
    // If there's a carry left, create a new node for it
    if (carry > 0) {
        current.next = new ListNode(carry);
    }
    
    return dummyHead.next; // Skip dummy node and return result list
}

```