//Given four integer arrays nums1, nums2, nums3, and nums4 all of length n, retu
//rn the number of tuples (i, j, k, l) such that: 
//
// 
// 0 <= i, j, k, l < n 
// nums1[i] + nums2[j] + nums3[k] + nums[l] == 0 
// 
//
// 
// Example 1: 
//
// 
//Input: nums1 = [1,2], nums2 = [-2,-1], nums3 = [-1,2], nums4 = [0,2]
//Output: 2
//Explanation:
//The two tuples are:
//1. (0, 0, 0, 1) -> nums1[0] + nums2[0] + nums3[0] + nums4[1] = 1 + (-2) + (-1)
// + 2 = 0
//2. (1, 1, 0, 0) -> nums1[1] + nums2[1] + nums3[0] + nums4[0] = 2 + (-1) + (-1)
// + 0 = 0
// 
//
// Example 2: 
//
// 
//Input: nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]
//Output: 1
// 
//
// 
// Constraints: 
//
// 
// n == nums1.length 
// n == nums2.length 
// n == nums3.length 
// n == nums4.length 
// 1 <= n <= 200 
// -228 <= nums1[i], nums2[i], nums3[i], nums4[i] <= 228 
// 
// Related Topics 哈希表 二分查找 
// 👍 353 👎 0

package leetcode.editor.cn;

import java.util.Map;
import java.util.HashMap;

//java:4Sum II
public class P454FourSumIi {
    public static void main(String[] args) {
        Solution solution = new P454FourSumIi().new Solution();
    }

    class Solution {
        public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
            int len = nums1.length;
            Map<Integer, Integer> sumOfTwoNums2Cnt = new HashMap<>();
            for (int i = 0; i < len; i ++) {
                for (int j = 0; j < len; j ++) {
                    sumOfTwoNums2Cnt.put(nums1[i] + nums2[j],
                            sumOfTwoNums2Cnt.getOrDefault(nums1[i] + nums2[j], 0) + 1);
                }
            }
            int tupleCnt = 0;
            for (int i = 0; i < len; i ++) {
                for (int j = 0; j < len; j ++) {
                    tupleCnt += sumOfTwoNums2Cnt.getOrDefault(-nums3[i] - nums4[j], 0);
                }
            }
            return tupleCnt;
        }
    }
}