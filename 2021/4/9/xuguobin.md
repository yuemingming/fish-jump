//Given an array of integers nums containing n + 1 integers where each integer i
//s in the range [1, n] inclusive. 
//
// There is only one repeated number in nums, return this repeated number. 
//
// 
// Example 1: 
// Input: nums = [1,3,4,2,2]
//Output: 2
// Example 2: 
// Input: nums = [3,1,3,4,2]
//Output: 31
// Example 3: 
// Input: nums = [1,1]
//Output: 1
// Example 4: 
// Input: nums = [1,1,2]
//Output: 1
// 
// 
// Constraints: 
//
// 
// 2 <= n <= 3 * 104 
// nums.length == n + 1 
// 1 <= nums[i] <= n 
// All the integers in nums appear only once except for precisely one integer wh
//ich appears two or more times. 
// 
//
// 
// Follow up: 
//
// 
// How can we prove that at least one duplicate number must exist in nums? 
// Can you solve the problem without modifying the array nums? 
// Can you solve the problem using only constant, O(1) extra space? 
// Can you solve the problem with runtime complexity less than O(n2)? 
// 
// Related Topics 数组 双指针 二分查找 
// 👍 1170 👎 0

package leetcode.editor.cn;

import java.util.Arrays;

//java:Find the Duplicate Number
public class P287FindTheDuplicateNumber {
    public static void main(String[] args) {
        Solution solution = new P287FindTheDuplicateNumber().new Solution();
    }

    class Solution {
        public int findDuplicate(int[] nums) {
            Arrays.sort(nums);
            int l = 0, r = nums.length - 1;
            while (l <= r) {
                int mid = (l + r) >> 1;
                if (mid - 1 < 0 || mid + 1 >= nums.length ||
                        nums[mid] == nums[mid - 1] || nums[mid] == nums[mid + 1]) 
                    return nums[mid];
                if (mid + 1 <= nums[mid]) l = mid + 1;
                else r = mid - 1;
            }
            return nums[l];
        }
    }

}