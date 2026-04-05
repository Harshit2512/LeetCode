- **Time complexity:** O(N)
- **Space complexity:** O(1)
- **Approach:**
    - Step - 1, find longest common prefix among all permutations (find a dip starting from the end)
    - Step - 2, swap dipped element with just greater element from right side array
    - Step - 3, place all other elements in increasing orser in right array (since we found longest prefix by dip, meaning all elements on right side are in increasing order starting from end, so now just reverse the right half to start right side after dip in shortest increasing order)


```java

class Solution {
    public void nextPermutation(int[] nums) {
        // Step - 1, find longest common prefix among all permutations (find a dip starting from the end)
        // Step - 2, swap dipped element with just greater element from right side array
        // Step - 3, place all other elements in increasing orser in right array (since we found longest prefix by dip, meaning all elements on right side are in increasing order starting from end, so now just reverse the right half to start right side after dip in shortest increasing order)

        int size = nums.length;
        int dipIndex = -1;

        // Step - 1, find dip
        for (int i = size - 2; i >= 0; i--) {
            if (nums[i] < nums[i + 1]) {
                dipIndex = i;
                break; 
            }
        }

        // If dipIndex is still -1 that means full array is in increasing order, so just need to reverse it
        if (dipIndex == -1) {
            reverseArray(nums, 0, size - 1);
        }

        // if dipIndex is not -1 means we need to find just greater element and swap with dipIndex (step 2 and 3)
        if (dipIndex != -1) {
            for (int i = size - 1; i > dipIndex; i--) {
            if (nums[i] > nums[dipIndex]) {
                int temp = nums[dipIndex];
                nums[dipIndex] = nums[i];
                nums[i] = temp;
                break;
            }
        }   
            
            // revrese right side array to make it next permutatin which is just greater
            reverseArray(nums, dipIndex + 1, size - 1);
        }    

    }

    void reverseArray(int[] arr, int start, int end) {
        while (start < end) {
            int temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;
            start++;
            end--;
        }
    }
}

```