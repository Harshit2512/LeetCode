- **Time Complexity:** O(N log N), each node is processed in O(log N) time and each call to find the middle takes linear time across all levels of the recursive tree.
- **Space Complexity:** O(log N), due to the recursion stack used during the divide process.
- **Key Points:**
    - Inorder traversal
    - Find the mid node using fast and slow  pointers
    - Devide from mid point and conquer using recusrsive approach to find left and right nodes of the root in the tree

```java
class Solution {
    public TreeNode sortedListToBST(ListNode head) {

        if (head == null) return null;
        
        return convertToBST(head, null);
    }

    private TreeNode convertToBST(ListNode head, ListNode tail) {

        if (head == tail) return null;

        ListNode fast = head;
        ListNode slow = head;

        while (fast != tail && fast.next != tail) {
            fast = fast.next.next;
            slow = slow.next;
        } 

        TreeNode node = new TreeNode(slow.val); 

        node.left = convertToBST(head, slow);
        node.right = convertToBST(slow.next, tail);

        return node;
    }
}
```