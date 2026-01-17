- **Approach:**
    - No need to useany other DS as underlying DS (like Queue). Just Define ListNode class to hold val and next pointer
    - For methods impl, use pointers accordingly and perform ops like add, get or delete
    - Note: (line 72) In for loop, your current node actually becomes a 1 index forward then index you're iterating. If at index 2 then current node after repointing is node at index 3
```java

class MyLinkedList {

    private class ListNode {
        int val;
        ListNode next;

        ListNode(int val) {
            this.val = val;
        }
    }

    private ListNode head;
    private int size;

    public MyLinkedList() {
        this.head = null;
        this.size = 0;
    }
    
    public int get(int index) {
        if (index < 0 || index >= size ) {
            return -1;
        }

        ListNode currentNode = head;
        for (int i = 0; i < index; i++) {
            currentNode = currentNode.next;
        }
        return currentNode.val;      
    }
    
    public void addAtHead(int val) {
        ListNode newNode = new ListNode(val);

        newNode.next = head;
        head = newNode;

        size++;        
    }
    
    public void addAtTail(int val) {
        ListNode newNode = new ListNode(val);
        
        if (head == null) {
            head = newNode;
        } else {
            ListNode currentNode = head;
            while (currentNode.next != null) {
                currentNode = currentNode.next;
            }
            currentNode.next = newNode;
        }
        size++;   
    }
    
    public void addAtIndex(int index, int val) {
        if (index > size) {
            return;
        }

        if (index <= 0) {
            addAtHead(val);
        } else {
            ListNode newNode = new ListNode(val);
            ListNode currentNode = head;
            // In for loop, your current node actually becomes a 1 index forward then index you're iterating. If at index 2 then current node after repointing is node at index 3
            // If ops needs to be done at index 3 then go only up to index 1. bcz at the end for fo loop, you will have access to node at index 2, and then node at index 3 can be access by index-2 node's next pointer
            for (int i = 0; i < index - 1; i++) {
                currentNode = currentNode.next;
            }
            newNode.next = currentNode.next;
            currentNode.next = newNode;
            size++;
        }
    }
    
    public void deleteAtIndex(int index) {
        if (index < 0 || index >= size) {
            return;
        }

        if (index == 0) {
            head = head.next;
        } else {
            ListNode currentNode = head;
            for (int i = 0; i < index - 1; i++) {
                currentNode = currentNode.next;
            }
            currentNode.next = currentNode.next.next;
        }
        size--;
    }
}

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList obj = new MyLinkedList();
 * int param_1 = obj.get(index);
 * obj.addAtHead(val);
 * obj.addAtTail(val);
 * obj.addAtIndex(index,val);
 * obj.deleteAtIndex(index);
 */

 ```