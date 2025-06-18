- **Time Complexity:**
    - Insert: O(n), where n is the length of the word to insert.
    - Search/StartsWith: O(n), where n is the length of the word/prefix to search.
- **Space Complexity:** In practice, it can be lower than using a fixed array due to dynamic allocation of children, especially if the set of possible characters is sparse.
- **Key Points:**
    - Use Hash Map for dynamic character store instead of fixed size list of 26 for chars

```java
class Trie {

    private static class TrieNode {
        Map<Character, TrieNode> map; // map to store dynamic children nodes for character
        boolean isEndOfWord;

        public TrieNode() {
            map = new HashMap<>();
            isEndOfWord = false;
        }
    }

    private final TrieNode root;

    public Trie() {
        root = new TrieNode();
    }
    
    public void insert(String word) {
        TrieNode current = root;
        for (char c : word.toCharArray()) {
            current.map.putIfAbsent(c, new TrieNode()); // Add tree node for this character
            current = current.map.get(c);
        }

        current.isEndOfWord = true; // mark if this trie node is end of word
    }
    
    public boolean search(String word) {
        TrieNode current = root;
        for (char c : word.toCharArray()) {
            current = current.map.get(c);
            if (current == null) {
                return false; // if trie node with this character not found, return false
            }
        }
        return current.isEndOfWord;
    }
    
    public boolean startsWith(String prefix) {
        TrieNode current = root;
        for (char c : prefix.toCharArray()) {
            current = current.map.get(c);
            if (current == null) {
                return false; // If character not found, then prefix doesn't match
            }
        }
        return true;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
 ```