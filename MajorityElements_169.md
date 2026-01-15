- **Time Complexity:** O(N)
- **Space Complexity:** O(1)
- **Approach:** Boyer-Moore voting algorithm
    - Define candidate and counter int variables
    - Candidate is the num which is eligible for max freq
    - If counter is 0 then assign current num as candidate.
    - If current num is same as candidate then increament counter or decrement counter. Final candidate value will be the answer

```java

class Solution {
    public int majorityElement(int[] nums) {

        // Boyer-Moore Voting Algorithm
        // https://github.com/AlgoMaster-io/leetcode-solutions/blob/main/java/majority-element.md

        int candidate = nums[0];
        int counter = 0;

        for (int num: nums) {
            if (counter == 0) {
                candidate = num;
            }

            counter = (num == candidate) ? counter + 1 : counter - 1;
            //counter += (num == candidate) ? 1 : -1;
        }

        return candidate;
    }
}

```