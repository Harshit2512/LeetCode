- https://github.com/AlgoMaster-io/leetcode-solutions/blob/main/java/maximum-number-of-balloons.md#approach-2-optimized-frequency-count-with-arrays
- **Time complexity:** O(n)
- **Space complexity:** O(1)

```java

class Solution {
    public int maxNumberOfBalloons(String text) {
        
        int[] freqArr = new int[26];

        for (char c : text.toCharArray()) {
            freqArr[c - 'a']++;
        }

        int maxBallon = Integer.MAX_VALUE;

        maxBallon = Math.min(maxBallon, freqArr['b' - 'a']);
        maxBallon = Math.min(maxBallon, freqArr['a' - 'a']);
        maxBallon = Math.min(maxBallon, freqArr['l' - 'a']/2);
        maxBallon = Math.min(maxBallon, freqArr['o' - 'a']/2);
        maxBallon = Math.min(maxBallon, freqArr['n' - 'a']);

        return maxBallon;

    }
}

```