//You are given a sorted array consisting of only integers where every element a
//ppears exactly twice, except for one element which appears exactly once. Find th
//is single element that appears only once. 
//
// Follow up: Your solution should run in O(log n) time and O(1) space. 
//
// 
// Example 1: 
// Input: nums = [1,1,2,3,3,4,4,8,8]
//Output: 2
// Example 2: 
// Input: nums = [3,3,7,7,10,11,11]
//Output: 10
// 
// 
// Constraints: 
//
// 
// 1 <= nums.length <= 10^5 
// 0 <= nums[i] <= 10^5 
// Related Topics 二分查找 
// 👍 216 👎 0

package leetcode.editor.cn;

//java:Single Element in a Sorted Array
public class P540SingleElementInASortedArray {
    public static void main(String[] args) {
        Solution solution = new P540SingleElementInASortedArray().new Solution();
    }

    class Solution {
        public int singleNonDuplicate(int[] nums) {
            if (nums == null || nums.length % 2 == 0) {
                return 0;
            }
            int l = 0, r = nums.length - 1;
            while (l <= r) {
                int mid = (l + r) >> 1;
                if (mid - 1 < 0 || mid + 1 >= nums.length) return nums[mid];
                int midNum = nums[mid];
                int midLeftNum = nums[mid - 1];
                int midRightNum = nums[mid + 1];
                if (midNum != midLeftNum && midNum != midRightNum) return nums[mid];
                if (midNum == midLeftNum) {
                    if (mid % 2 == 0) r = mid - 1;
                    else l = mid + 1;
                } else {
                    if (mid % 2 == 0) l = mid + 1;
                    else r = mid - 1;
                }
            }
            return nums[l];
        }
    }
}