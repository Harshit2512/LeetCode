- **Time Complexity:** O(m + n log n), where m is the length of the searchWord, and n is the number of products. Sorting takes O(n log n), and the search using two pointers costs O(m) for narrowing the range for each prefix.
- **Space Complexity:** O(1) (apart from the space needed for output), since we are not using extra space for structures other than the list for output.
- **Key Points:**
    - Use two pointers approach for setting correct range window in products which matches chars in given searchWord
    - Get all next three lexicographical products from window range for each prefix chars

```java
class Solution {
    public List<List<String>> suggestedProducts(String[] products, String searchWord) {
        Arrays.sort(products); // Sort array for lexicographical order
        List<List<String>> result = new ArrayList<>();

        // set left and right window range
        int left = 0;
        int right = products.length - 1;

        for (int i = 0; i < searchWord.length(); i++) {
            // List for word suggestions for each character in searchWord
            List<String> suggestions = new ArrayList<>();
            char c = searchWord.charAt(i);

            // pointers move conditions for getting valid window
            while (left <= right && (products[left].length() <= i || products[left].charAt(i) != c)) {
                left++;
            }

            while (left <= right && (products[right].length() <= i || products[right].charAt(i) != c)) {
                right--;
            }

            // Get only next three suggestions
            for (int j = left; j < Math.min(left + 3, right + 1); j++) {
                suggestions.add(products[j]);
            }

            result.add(suggestions);
        }

        return result;
    }
}
```