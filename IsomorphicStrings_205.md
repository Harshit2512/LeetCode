- **Time Complexity:** O(n), where n is the length of the string. We iterate through each character once
- **Space Complexity:** O(1), specifically O(26) if considering distinct lowercase letters. In practice, the space used by hash maps is relative to the character set
- **Key Value:**
    - Create two hash maps
    - For each character in s and t, ensure the mapping is unique and consistent in both directions (charS -> charT and charT -> charS)

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        
        if (s.length() != t.length()) return false;

        Map<Character, Character> mapST = new HashMap<>();
        Map<Character, Character> mapTS = new HashMap<>();

        for (int i = 0; i < s.length(); i++) {
            char S = s.charAt(i);
            char T = t.charAt(i);

            if (mapST.containsKey(S)) {
                if (mapST.get(S) != T) return false; 
            } else {
                mapST.put(S, T);
            }

            if (mapTS.containsKey(T)) {
                if (mapTS.get(T) != S) return false; 
            } else {
                mapTS.put(T, S);
            }
        } 
        
        return true;
    }
}
```