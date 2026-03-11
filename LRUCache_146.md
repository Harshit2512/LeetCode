- **Time Complexity:** O(1) for both get and put operations as we continue to have constant time hash table and linked list operations.
- **Space Complexity:** O(capacity) for storing the elements and linked list pointers.
- **Approach: Doubly Linked List with HashMap**
    - Use a doubly linked list to maintain the order of use of the cache and a HashMap for quick access to elements. The doubly linked list maintains a list of nodes, each representing a key-value pair. The head of the list is the most recently used, and the tail is the least used.
    - Use a doubly linked list because it provides constant time access to update and remove nodes.
    - Use a HashMap to store references to the nodes of the linked list with the key-value pairs so that we can achieve O(1) time complexity for get and put operations.
    - When a key is accessed or added, move it to the head of the list. This denotes that it's the most recently used.
    - Upon hitting capacity, remove the node at the tail (least recently used).


```java

class LRUCache {

    Map<Integer, Node> cache;
    int capacity;
    Node head;
    Node tail;

    // constructor to initialize new cache and DDL
    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.cache = new HashMap<>();
        this.head = new Node(0, 0);
        this.tail = new Node(0, 0);

        // create initial connection between dummy head and tail
        this.head.next = this.tail;
        this.tail.prev = this.head;
    }
    
    public int get(int key) {
        Node node = cache.get(key);

        // Check if cache has this node by key already present
        if (node != null) {
            // case - cache has this key
            // Since recently accessed, move node after head
            insertAfterHead(node);
            return node.value;
        } else {
            // key not present in cache, return -1
           return -1; 
        }
    }
    
    public void put(int key, int value) {
        // // Create new node first
        Node node = cache.get(key);

        if (node != null) {
            // Update node value to new value in cache
            node.value = value;
            // No need to perform put op again - cache.put(key, node);
            
            // Since recently accessed, move node after head
            insertAfterHead(node);
        } else {
            Node newNode = new Node(key, value);
            cache.put(key, newNode);
            insert(newNode);
        }

        // Check the size of the cache, if greater than capacity then remove node before tail (last node which is least recently used)
        if (cache.size() > capacity) {
            // popTail to remove las node node (LRU) from DLL
            Node removedNode = popTail();

            // Also remove node entry from cache
            cache.remove(removedNode.key);
        }
    }

    public void insertAfterHead(Node node) {
        remove(node);
        insert(node);
    }

    public Node popTail() {
        Node lastNode = tail.prev;
        remove(lastNode);
        return lastNode;
    }

    public void remove(Node node) {
        // current pointers
        Node next = node.next;
        Node prev = node.prev;

        // update pointers after removing node
        prev.next = next;
        next.prev= prev;
    }

    public void insert(Node node) {
        // First create links for new node 
        node.next = head.next;
        node.prev = head;

        // update current head and node's links to new node
        head.next.prev = node;
        head.next = node;
    }


}

class Node {
    int key;
    int value;
    Node next;
    Node prev;

    // create stand-alone node
    Node(int key, int value) {
        this.key = key;
        this.value = value;
        this.next = null;
        this.prev = null;
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */

 ```