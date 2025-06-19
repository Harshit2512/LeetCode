- **Time Complexity:** O(m) for adding and typical search where m is the length of the word.
- **Space Complexity:** O(n * m) where n is the number of words and m is the average length of words to store the Trie.
- **Key Points:**
    - Use Trie DS which is efficient at prefix search

```java
class WordDictionary {

     private static class TrieNode {
        private TrieNode[] children;
        private boolean isEndOfWord;

        public TrieNode() {
            children = new TrieNode[26]; // 26 children for each letter 'a' to 'z'
            isEndOfWord = false; // True if the node represents the end of a word
        }
    }

    private TrieNode root;


    public WordDictionary() {
        root = new TrieNode();
    }
    
    public void addWord(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            int index = c - 'a';
            if (node.children[index] == null) { //if node is not present
                node.children[index] = new TrieNode(); // Add new node for character c
            }
            node = node.children[index];
        }
        node.isEndOfWord = true; 
    }
    
    public boolean search(String word) {
        return searchWord(word, root, 0);
    }

    boolean searchWord(String word, TrieNode node, int pos) {
        if (pos == word.length()) {
            return node.isEndOfWord;
        }

        char c = word.charAt(pos);
        if (c == '.') { // try out each child node if char is wild card
            for (TrieNode child : node.children) {
                if (child != null && searchWord(word, child, pos + 1)) {
                    return true;
                }
            }
            return false;
        } else { // else if specific char
            int index = c - 'a';
            return node.children[index] != null && searchWord(word, node.children[index], pos + 1);
        }
    }
}

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * boolean param_2 = obj.search(word);
 */
 ```