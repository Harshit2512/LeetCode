- **Time Complexity:** O(NK log K) where N is the number of strings and K is the maximum length of a string. Sorting each string takes O(K log K).
- **Space Complexity:** O(NK), the space for storing the groups of anagrams.
- **Approach:** Sorting Each word and using HashMap [key: sorted string, value: all anagrams]
    - Iterate each string in array and sort char withing string
    - Store sorted str as key and value as actual string. (For each anagram, sorted str becomes same so that goes as key of the map and value is all anagrams)
    - Return map value as array list 

```java

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        // Map to store the list of anagrams
        Map<String, List<String>> anagramMap = new HashMap<>();
        
        for (String word : strs) {
            // Convert the word to an array of characters
            char[] charArray = word.toCharArray();
            // Sort the array
            Arrays.sort(charArray);
            // Convert back to string
            String sortedWord = new String(charArray);
            
            // If the sorted word is not in the map, add it with an empty list
            if (!anagramMap.containsKey(sortedWord)) {
                anagramMap.put(sortedWord, new ArrayList<>());
            }
            
            // Append the original word to the corresponding list
            anagramMap.get(sortedWord).add(word);
        }
        
        // Return the grouped list of anagrams
        return new ArrayList<>(anagramMap.values());
    }
}

```