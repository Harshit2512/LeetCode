- **Time Complexity:** O(N log k), as we perform heap operations (insertions/deletions) proportional to the number of unique words, where each operation takes O(log k).
- **Space Complexity:** O(N), for storing the hashmap and the heap potentially containing all unique words.
- **Key Points:**
    - In case of equal freq, to maintain lexicographical order, use comparator condition --> a.compareTo(b)
    - Find the strings frequency first
    - Use PQ with custom sorting to always keep higher freq string at the head
    - Build result string array by getting each string from PQ

```java

class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        
        Map<String, Integer> frequencyMap = new HashMap<>();
        // Priority Queue to sort strings by frequency keeping max at head
        PriorityQueue<String> maxHeap = new PriorityQueue<>((a, b) -> frequencyMap.get(b).equals(frequencyMap.get(a)) 
                    ? a.compareTo(b) 
                    : frequencyMap.get(b) - frequencyMap.get(a));

        // First count the frequency of each chanracter in string
        for (String c : words) {
            frequencyMap.put(c, frequencyMap.getOrDefault(c, 0) + 1);
        }

        // Add all strings in PQ, arranged in sorting order to keep string with highest freq at head
        maxHeap.addAll(frequencyMap.keySet());

        List<String> result = new ArrayList<>();
        int i = 0;
        while (i < k) {
            result.add(maxHeap.poll());
            i++;
        }

        return result;

        // ----------------------------------------------------------------------------------------------------------------------------
        // Using Min - Heap PQ implementation
        //     // Step 1: Frequency mapping
        // Map<String, Integer> count = new HashMap<>();
        // for (String word : words) {
        //     count.put(word, count.getOrDefault(word, 0) + 1);
        // }
        
        // // Step 2: Min-Heap to store top k frequent words
        // PriorityQueue<String> heap = new PriorityQueue<>(
        //     (w1, w2) -> count.get(w1).equals(count.get(w2)) 
        //                 ? w2.compareTo(w1) 
        //                 : count.get(w1) - count.get(w2));
        
        // for (String word : count.keySet()) {
        //     heap.offer(word);
        //     if (heap.size() > k) {
        //         heap.poll(); // Remove the word with the smallest frequency
        //     }
        // }
        
        // // Step 3: Form result list from the heap
        // List<String> result = new ArrayList<>();
        // while (!heap.isEmpty()) {
        //     result.add(heap.poll());
        // }
        // Collections.reverse(result); // Since we want the largest frequencies first
        // return result;
    }
}

```