//You are given an integer array nums where the ith bag contains nums[i] balls. 
//You are also given an integer maxOperations. 
//
// You can perform the following operation at most maxOperations times: 
//
// 
// Take any bag of balls and divide it into two new bags with a positive number 
//of balls.
//
// 
// For example, a bag of 5 balls can become two new bags of 1 and 4 balls, or tw
//o new bags of 2 and 3 balls. 
// 
// 
// 
//
// Your penalty is the maximum number of balls in a bag. You want to minimize yo
//ur penalty after the operations. 
//
// Return the minimum possible penalty after performing the operations. 
//
// 
// Example 1: 
//
// 
//Input: nums = [9], maxOperations = 2
//Output: 3
//Explanation: 
//- Divide the bag with 9 balls into two bags of sizes 6 and 3. [9] -> [6,3].
//- Divide the bag with 6 balls into two bags of sizes 3 and 3. [6,3] -> [3,3,3]
//.
//The bag with the most number of balls has 3 balls, so your penalty is 3 and yo
//u should return 3.
// 
//
// Example 2: 
//
// 
//Input: nums = [2,4,8,2], maxOperations = 4
//Output: 2
//Explanation:
//- Divide the bag with 8 balls into two bags of sizes 4 and 4. [2,4,8,2] -> [2,
//4,4,4,2].
//- Divide the bag with 4 balls into two bags of sizes 2 and 2. [2,4,4,4,2] -> [
//2,2,2,4,4,2].
//- Divide the bag with 4 balls into two bags of sizes 2 and 2. [2,2,2,4,4,2] ->
// [2,2,2,2,2,4,2].
//- Divide the bag with 4 balls into two bags of sizes 2 and 2. [2,2,2,2,2,4,2] 
//-> [2,2,2,2,2,2,2,2].
//The bag with the most number of balls has 2 balls, so your penalty is 2 an you
// should return 2.
// 
//
// Example 3: 
//
// 
//Input: nums = [7,17], maxOperations = 2
//Output: 7
// 
//
// 
// Constraints: 
//
// 
// 1 <= nums.length <= 105 
// 1 <= maxOperations, nums[i] <= 109 
// 
// Related Topics 堆 二分查找 
// 👍 32 👎 0

package leetcode.editor.cn;

import java.util.Arrays;

//java:Minimum Limit of Balls in a Bag
public class P1760MinimumLimitOfBallsInABag {
    public static void main(String[] args) {
        Solution solution = new P1760MinimumLimitOfBallsInABag().new Solution();
    }

    class Solution {
        public int minimumSize(int[] nums, int maxOperations) {
            int l = 1, r = findMax(nums);
            int res = 0;
            while (l <= r) {
                int mid = (l + r) >> 1;
                long operation = 0;
                for (int num : nums) {
                    operation += (num - 1) / mid;
                }
                if (operation <= maxOperations) {
                    res = mid;
                    r = mid - 1;
                } else {
                    l = mid + 1;
                }
            }
            return res;
        }

        private int findMax(int[] nums) {
            return Arrays.stream(nums).max().orElse(0);
        }
    }
}