- **Time Complexity:** O(2^n) - where n is the number of elements in nums. Each element can either be included or not included, leading to 2^n possible subsets.
- **Space Complexity:** O(n) - space used by the recursion stack.

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(0, nums, result, new ArrayList<>());
        return result;
    }

    private void backtrack(int start, int[] nums, List<List<Integer>> result, List<Integer> path) {

        result.add(new ArrayList<>(path));

        for (int i = start; i < nums.length; i++) {
            path.add(nums[i]);
            backtrack(i + 1, nums, result, path);
            path.remove(path.size() - 1);
        }        
    }
}
```