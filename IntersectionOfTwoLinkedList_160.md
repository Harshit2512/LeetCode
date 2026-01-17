- **Approach:** Using Two Pointer Technique
- Time Complexity: O(m + n), where m and n are the lengths of the two linked lists.
- Space Complexity: O(1), as no extra space is used, just pointers are moved
- **Steps:**
    - Keep iterating two linked list until two nodes are same (means converges). 
    - While iterating, if listA pointer reaches to end (null node) then point to listB head headB and vice versa.
    - Eventually both poiter will meet to same node value. That's the intersection node

```java

public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        // If either head is null, they cannot intersect
        if (headA == null || headB == null) {
            return null;
        }
        
        ListNode a = headA;
        ListNode b = headB;
        
        // Loop until the pointers meet or both reach to end
        while (a != b) {
            a = (a == null) ? headB : a.next;
            b = (b == null) ? headA : b.next;
        }
        
        // Either they met at intersection node or both are null
        return a;
    }
}

```

- **Approach:** Using HashSet
- **Steps:**
    - Traverse through the second list and add its nodes to the hashset
    - Traverse through the first list and check if any node is in the hashset. If set contains node, it's the intersection node
- **Time Complexity:** O(m + n), where m and n are the lengths of the two linked lists
- **Space Complexity:** O(n), where n is the length of the longer linked list since all its nodes are stored in a set
- Put longer linked List in a set and then iterate each node of other list and check if it exists in set, if exists then it's common node

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        HashSet<ListNode> nodesInB = new HashSet<>();
        
        // Traverse through the second list and add its nodes to the hashset
        ListNode b = headB;
        while (b != null) {
            nodesInB.add(b);
            b = b.next;
        }
        
        // Traverse through the first list and check if any node is in the hashset
        ListNode a = headA;
        while (a != null) {
            if (nodesInB.contains(a)) {
                return a; // Found intersection
            }
            a = a.next;
        }
        
        return null; // No intersection found
    }
}

```