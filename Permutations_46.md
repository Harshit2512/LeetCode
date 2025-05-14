- **Time Complexity:** O(n * n!), n is the numbers in array and n! is the permutation using n numbers
- **Space Complexity:** O(n), recursive call stack for n numbers used for permutation
**Key Points:**
    - Iterate each number and permute with every other numbers in array
    - Check if number is used in permutation, if not used them add in temp list and then backtrack

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(nums, result, new ArrayList<>(), new boolean[nums.length]);
        return result;
    }

    private void backtrack(int[] nums, List<List<Integer>> result, List<Integer> tempList, boolean[] used) {

        // Base case: breaking condition when pair has been made and need to add in final result
        if (tempList.size() == nums.length) {
            result.add(new ArrayList<>(tempList));
            return;
        } else {

            // Interate each number in array
            for (int i = 0; i < nums.length; i++) {

                // If number is already used in permutation then ignore
                if (used[i]) continue;
                
                // If not used, use number in permutation
                used[i] = true;
                tempList.add(nums[i]);

                // backtack
                backtrack(nums, result, tempList, used);

                // undo the decision
                used[i] = false;
                tempList.remove(tempList.size() - 1);
            }
        }
    }
}
```