- **Time Complexity** = O(N) 
- **Space complexity** = O(1)
- **Approach:** Clone LL in-place, assign random pointers and detach copied list
    - Step-1: create a copy of the original node and place it after original node by changing connection, without assigning random ref value
    - Step - 2: Assign random value of the node
    - Step - 3: Detach the the new linked list from original list  by changing refs of original and new linked list

```java

/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/

class Solution {
    public Node copyRandomList(Node head) {

        // edge case where list is null
        if (head == null) {
            return null;
        }

        // Step-1: create a copy of the original node and place it after original node by changing connection, without assigning random ref value
        Node current = head;
        while (current != null) {
            Node newNode = new Node(current.val);
            newNode.next = current.next;
            current.next = newNode;
            current = newNode.next;
        }

        // Step - 2: Assign random value of the node
        Node current1 = head;
        while (current1 != null) {
            if (current1.random != null) {
                current1.next.random = current1.random.next;
            }
            current1 = current1.next.next;
        }

        // Step - 3: Detach the the new linked list from original list  by changing refs of original and new linked list
        Node curr2 = head;
        Node newCurr = curr2.next;
        Node newHead = newCurr;
        while (curr2 != null) {
            curr2.next = newCurr.next;
            curr2 = newCurr.next;
            if (curr2 != null) {
                newCurr.next = curr2.next;
                newCurr = curr2.next;
            }        
        }
        return newHead;       
    }
}

```