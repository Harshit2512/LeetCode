- **Time Complexity:** O(log N) where N is the number of elements in a bucket.
- **Space Complexity:** O(N) where N is the total number of elements.
- **Solution:** using BST
    - https://github.com/AlgoMaster-io/leetcode-solutions/blob/main/java/design-hashmap.md#approach-3-binary-search-tree-in-buckets



```java

class MyHashMap {

    private final int SIZE = 1000;
    TreeMap<Integer, Integer>[] map;
    public MyHashMap() {
        map = new TreeMap[SIZE];
    }

    private int getHash(int key) {
        return Integer.hashCode(key) % SIZE;
    }
    
    public void put(int key, int value) {
        int index = getHash(key);
        if (map[index] == null) {
            map[index] = new TreeMap<>();
        }
        map[index].put(key, value);
    }
    
    public int get(int key) {
        int index = getHash(key);
        return map[index] != null ? map[index].getOrDefault(key, -1) : -1;
    }
    
    public void remove(int key) {
        int index = getHash(key);
        if (map[index] != null) {
            map[index].remove(key);
        }
    }
}

/**
 * Your MyHashMap object will be instantiated and called as such:
 * MyHashMap obj = new MyHashMap();
 * obj.put(key,value);
 * int param_2 = obj.get(key);
 * obj.remove(key);
 */

 ```