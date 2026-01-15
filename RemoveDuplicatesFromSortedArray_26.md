- **Time Complexity:** O(N)
- **Space Complexity:** O(1)
- **Approach:** Array using two pointers (readPos and writePos)
    - Keep writePos at index 0 and keep moving readPos until element at writePos and readPos is same
    - When readPos is different than writePos then move element at readPos to writePos.
    - Return writePos + 1, which is length of array with all unique elements
    - https://algomaster.io/animations/dsa/remove-duplicates

```java

class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;

        int writePos = 0;
        for (int readPos = 1; readPos < nums.length; readPos++) {
            if (nums[readPos] != nums[writePos]) {
                writePos++;
                nums[writePos] = nums[readPos];
            }
        }

        return writePos + 1;
    }
}


// My solution - Easy and straight forward
class Solution {
    public int removeDuplicates(int[] nums) {
          
        int placeNum = 1;
        
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] > nums[i-1]) {
                
                nums[placeNum] = nums[i];
                placeNum++;
            }
        }

        return placeNum;
    }
}

```

