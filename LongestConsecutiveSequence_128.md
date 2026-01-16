- **Time complexity**: O(N), where N is the length of the array due to one pass through the elements and constant time lookups.
- **Space complexity**: O(N), because of the space used by the HashSet.
- **Approach:**
    - Add numbers to HashSet: This allows constant-time lookups.
    - At each number, check if n-1 exists in set and num is beginning of sequence. If yes then current number is already part of other sequence. If not then start new sequence.
    - Maintain currentNum and currentStreak for that number by checking n+1 present using while loop. And update longestStreak by taking max of current and longest streak
    - Return longestStreak at the end

```java

public int longestConsecutive(int[] nums) {
    if (nums.length == 0) return 0;

    Set<Integer> numSet = new HashSet<>();
    for (int num : nums) {
        numSet.add(num);
    }

    int longestStreak = 0;

    for (int num : numSet) {
        // Check if num is the beginning of a sequence
        if (!numSet.contains(num - 1)) {
            int currentNum = num;
            int currentStreak = 1;

            // Increment currentNum to count the length of sequence
            while (numSet.contains(currentNum + 1)) {
                currentNum += 1;
                currentStreak += 1;
            }

            longestStreak = Math.max(longestStreak, currentStreak);
        }
    }
    return longestStreak;
}

```