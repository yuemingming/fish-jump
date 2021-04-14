//Koko loves to eat bananas. There are n piles of bananas, the ith pile has pile
//s[i] bananas. The guards have gone and will come back in h hours. 
//
// Koko can decide her bananas-per-hour eating speed of k. Each hour, she choose
//s some pile of bananas and eats k bananas from that pile. If the pile has less t
//han k bananas, she eats all of them instead and will not eat any more bananas du
//ring this hour. 
//
// Koko likes to eat slowly but still wants to finish eating all the bananas bef
//ore the guards return. 
//
// Return the minimum integer k such that she can eat all the bananas within h h
//ours. 
//
// 
// Example 1: 
//
// 
//Input: piles = [3,6,7,11], h = 8
//Output: 4
// 
//
// Example 2: 
//
// 
//Input: piles = [30,11,23,4,20], h = 5
//Output: 30
// 
//
// Example 3: 
//
// 
//Input: piles = [30,11,23,4,20], h = 6
//Output: 23
// 
//
// 
// Constraints: 
//
// 
// 1 <= piles.length <= 104 
// piles.length <= h <= 109 
// 1 <= piles[i] <= 109 
// 
// Related Topics 二分查找 
// 👍 162 👎 0

package leetcode.editor.cn;

//java:Koko Eating Bananas
public class P875KokoEatingBananas {
    public static void main(String[] args) {
        Solution solution = new P875KokoEatingBananas().new Solution();
        int[] nums = {30,11,23,4,20};
        System.out.println(solution.minEatingSpeed(nums, 6));
    }

    class Solution {
        public int minEatingSpeed(int[] piles, int h) {
            int minSpeed = 1, maxSpeed = findMax(piles);
            int res = 0;
            while (minSpeed <= maxSpeed) {
                int speed = (minSpeed + maxSpeed) >> 1;
                long costHour = 0;
                for (int pile : piles) {
                    costHour += pile / speed;
                    costHour += pile % speed == 0 ? 0 : 1;
                }
                if (costHour <= h) {
                    res = speed;
                    maxSpeed = speed - 1;
                } else {
                    minSpeed = speed + 1;
                }
            }
            return res;
        }

        private int findMax(int[] nums) {
            int res = Integer.MIN_VALUE;
            for (int num : nums) res = Math.max(num, res);
            return res;
        }
    }
}