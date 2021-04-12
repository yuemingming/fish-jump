//Winter is coming! During the contest, your first job is to design a standard h
//eater with a fixed warm radius to warm all the houses. 
//
// Every house can be warmed, as long as the house is within the heater's warm r
//adius range. 
//
// Given the positions of houses and heaters on a horizontal line, return the mi
//nimum radius standard of heaters so that those heaters could cover all houses. 
//
// Notice that all the heaters follow your radius standard, and the warm radius 
//will the same. 
//
// 
// Example 1: 
//
// 
//Input: houses = [1,2,3], heaters = [2]
//Output: 1
//Explanation: The only heater was placed in the position 2, and if we use the r
//adius 1 standard, then all the houses can be warmed.
// 
//
// Example 2: 
//
// 
//Input: houses = [1,2,3,4], heaters = [1,4]
//Output: 1
//Explanation: The two heater was placed in the position 1 and 4. We need to use
// radius 1 standard, then all the houses can be warmed.
// 
//
// Example 3: 
//
// 
//Input: houses = [1,5], heaters = [2]
//Output: 3
// 
//
// 
// Constraints: 
//
// 
// 1 <= houses.length, heaters.length <= 3 * 104 
// 1 <= houses[i], heaters[i] <= 109 
// 
// Related Topics 二分查找 
// 👍 190 👎 0

package leetcode.editor.cn;

import java.util.Arrays;

//java:Heaters
public class P475Heaters {
    public static void main(String[] args) {
        Solution solution = new P475Heaters().new Solution();
    }

    class Solution {

        private int[] heaters;

        public int findRadius(int[] houses, int[] heaters) {
            this.heaters = heaters;
            Arrays.sort(heaters);
            int minRadius = Integer.MIN_VALUE;
            for (int house : houses) {
                minRadius = Math.max(minRadius, findMinRadius(house));
            }
            return minRadius;
        }

        private int findMinRadius(int house) {
            int l = 0, r = heaters.length - 1;
            while (l <= r) {
                int mid = (l + r) >> 1;
                int heater = heaters[mid];
                if (heater == house) {
                    return 0;
                } else if (heater < house) {
                    if (mid >= heaters.length - 1) {
                        return house - heater;
                    } else {
                        int nextHeater = heaters[mid + 1];
                        if (nextHeater < house) {
                            l = mid + 2;
                        } else {
                            return Math.min(house - heater, nextHeater - house);
                        }
                    }
                } else {
                    if (mid <= 0) {
                        return heater - house;
                    } else {
                        int preHeater = heaters[mid - 1];
                        if (preHeater > house) {
                            r = mid - 2;
                        } else {
                            return Math.min(house - preHeater, heater - house);
                        }
                    }
                }
            }
            return l > heaters.length - 1 ? house - heaters[heaters.length - 1] : heaters[0] - house;
        }
    }
}