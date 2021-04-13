//Given two integer arrays A and B, return the maximum length of an subarray tha
//t appears in both arrays. 
//
// Example 1: 
//
// 
//Input:
//A: [1,2,3,2,1]
//B: [3,2,1,4,7]
//Output: 3
//Explanation: 
//The repeated subarray with maximum length is [3, 2, 1].
// 
//
// 
//
// Note: 
//
// 
// 1 <= len(A), len(B) <= 1000 
// 0 <= A[i], B[i] < 100 
// 
//
// 
// Related Topics 数组 哈希表 二分查找 动态规划 
// 👍 423 👎 0

package leetcode.editor.cn;

//java:Maximum Length of Repeated Subarray
public class P718MaximumLengthOfRepeatedSubarray {
    
    public static void main(String[] args) {
        Solution solution = new P718MaximumLengthOfRepeatedSubarray().new Solution();
    }

    class Solution {
        
        public int findLength(int[] A, int[] B) {
            if (A == null || B == null || A.length == 0 || B.length == 0) return 0;
            int[][] dp = initDP(A, B);
            for (int i = 1; i < A.length; i++) {
                for (int j = 1; j < B.length; j++) {
                    int numOfA = A[i], numOfB = B[j];
                    dp[i][j] = numOfA == numOfB ? dp[i - 1][j - 1] + 1 : 0;
                }
            }
            return findMaxValueFromDP(dp);
        }

        private int findMaxValueFromDP(int[][] dp) {
            int res = 0;
            for (int[] nums : dp)
                for (int num : nums)
                    res = Math.max(res, num);
            return res;
        }

        private int[][] initDP(int[] a, int[] b) {
            int[][] dp = new int[a.length][b.length];
            int firstNumOfA = a[0], firstNumOfB = b[0];
            for (int i = 0; i < b.length; i++) {
                dp[0][i] = b[i] == firstNumOfA ? 1 : 0;
            }
            for (int i = 0; i < a.length; i++) {
                dp[i][0] = a[i] == firstNumOfB ? 1 : 0;
            }
            return dp;
        }
    }
}