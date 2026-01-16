- **Time complexity** = O(3^N * 4^M) where N is the number of digits in the input that maps to 3 digits like 2,3,4,5,6,8
- **Space complexity** = O(3^N * 4^M) since one has to keep 3^N * 4^M solutions
- https://www.youtube.com/watch?v=imD5XeNaJXA - Nick White
- **Solution:** Queue using Linked List - Iterative way to find combination
    - Define output linked list and add "" in it
    - When current iterated index is equal to peeked element length from Queue, run while loop to create permution of all chars with peeked element
    - when output.peek().length() == i, permutation = element (combChar) + char

```java

class Solution {
    public List<String> letterCombinations(String digits) {
        LinkedList<String> output = new LinkedList();
        String[] mapping = new String[] {"0", "1", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        if(digits.length() == 0) return output;

        output.add("");

        for (int i = 0; i < digits.length(); i++) {
            int number = Character.getNumericValue(digits.charAt(i));
            while (output.peek().length() == i) {
                String combChar = output.remove();
                for (char c : mapping[number].toCharArray()) {
                    output.add(combChar + c);
                }
            } 
        } 

        return output;  
    }
}

```