- **Time complexity** = O(N), where N is the total number of nodes because each node is visited once.
- **Space complexity** = O(N) in the worst case due to the recursive function call stack.
- KP:
    - How to write the recursive function
    - How to and where to link the child list with main list 


```java

/*
// Definition for a Node.
class Node {
    public int val;
    public Node prev;
    public Node next;
    public Node child;
};
*/

class Solution {
    public Node flatten(Node head) {
        flattenHelper(head);
        return head;       
    }

    private Node flattenHelper(Node node) {
        Node curr = node;
        Node last = node;

        while (curr != null) {
            Node next = curr.next;

            if (curr.child != null) {
                Node childLast = flattenHelper(curr.child);

                // connect beginning of child list to main list
                curr.next = curr.child;
                curr.child.prev = curr;
                curr.child = null;

                // connect end of child list to main list
                if (next != null) {
                    childLast.next = next;
                    next.prev = childLast;
                }      
                last = childLast;

            } else {
                last = curr;
            }
            curr = next;
        }

        return last;
    } 
}

```