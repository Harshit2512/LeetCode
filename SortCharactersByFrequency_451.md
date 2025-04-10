- **Time complexity:** O(n log k), where n is the number of characters and k is the unique characters (k ≤ n).
- **Space Complexity:** O(n) - for the max-heap and the result string.
- **Key Points:**
    - Find the character frequency first
    - Use PQ with custom sorting to always keep higher freq char at the head
    - Build result string by getting each char from PQ and taking it's freq from freq map

```java
    
class Solution {
    public String frequencySort(String s) {

        Map<Character, Integer> frequencyMap = new HashMap<>();
        // Priority Queue to sort chars by frequency keeping max at head
        PriorityQueue<Character> maxHeap = new PriorityQueue<>((a, b) -> frequencyMap.get(b) - frequencyMap.get(a));

        // First count the frequency of each chanracter in string
        for (char c : s.toCharArray()) {
            frequencyMap.put(c, frequencyMap.getOrDefault(c, 0) + 1);
        }

        // Add all characters in PQ, arranged in sorting order to keep char with highest freq at head
        maxHeap.addAll(frequencyMap.keySet());

        StringBuilder sb = new StringBuilder();

        while (!maxHeap.isEmpty()) {
            char c = maxHeap.poll();
            // Append char as many times of frequency from frequency map
            for (int i = 0; i < frequencyMap.get(c); i++) {
                sb.append(c);
            }
        }

        return sb.toString();      
    }
}

```