- **Time Complexity:** O(N * M * 26) where N is the number of words in the word list and M is the length of each word. For every word, in the worst case, we change each character (M) to every other character in the alphabet (26 possibilities).
- **Space Complexity:** O(N * M) for the wordSet and queue data structures.
- **Key Points:**
    - Problem can be seen as graph where each word represent node and diff of char between adj words as edge
    - Load wordList to Set to search word by O(1) and load beginWord in queue
    - Iterate each character in a word and replace with all 26 alphabets (all possible combination for new char) to create a new word
    - If new word is present in word set then place new word in queue and remove from wordSet
    - If by replacing char, newWord is same as lastWord then we reached to end (shortest path) and return level
    - At each queue word traversal, increase level 

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> words = new HashSet<>(wordList); // Load wordList to Set to search word by O(1)
        Queue<String> queue = new LinkedList<>();
        int level = 1;
        // if endWord is not in wordList then return 0
        if (!words.contains(endWord)) return 0;

        queue.offer(beginWord);

        while (!queue.isEmpty()) {
            int size = queue.size();
            
            // iterate each word in queue
            for (int i = 0; i < size; i++) {
                String currentWord = queue.poll();
                char[] wordArray = currentWord.toCharArray();

                // iterate each character in a word and replace with all 26 alphabets to create a new word
                for (int charIdx = 0; charIdx < wordArray.length; charIdx++) {
                    char originalChar = wordArray[charIdx];
                    for (char c = 'a'; c <= 'z'; c++) {
                        // if same character then skip it
                        if (wordArray[charIdx] == c) continue;
                        wordArray[charIdx] = c;
                        String newWord = new String(wordArray);

                        // if by replacing char, newWord is same as lastWord then we reached to end (shortest path) and return level
                        if (newWord.equals(endWord)) {
                            return level + 1; // shortest path found
                        }

                        if (words.contains(newWord)) {
                            queue.offer(newWord);
                            words.remove(newWord); //remove to prevel revisitng
                        }  
                    }
                    // restore original letter for next iteration
                    wordArray[charIdx] = originalChar;
                }
                
            }
            level++; //increament level
        }
        return 0; // If endWord is not reachable from beginWord
    }
}
```