//You are given an array of intervals, where intervals[i] = [starti, endi] and e
//ach starti is unique. 
//
// The right interval for an interval i is an interval j such that startj >= end
//i and startj is minimized. 
//
// Return an array of right interval indices for each interval i. If no right in
//terval exists for interval i, then put -1 at index i. 
//
// 
// Example 1: 
//
// 
//Input: intervals = [[1,2]]
//Output: [-1]
//Explanation: There is only one interval in the collection, so it outputs -1.
// 
//
// Example 2: 
//
// 
//Input: intervals = [[3,4],[2,3],[1,2]]
//Output: [-1,0,1]
//Explanation: There is no right interval for [3,4].
//The right interval for [2,3] is [3,4] since start0 = 3 is the smallest start t
//hat is >= end1 = 3.
//The right interval for [1,2] is [2,3] since start1 = 2 is the smallest start t
//hat is >= end2 = 2.
// 
//
// Example 3: 
//
// 
//Input: intervals = [[1,4],[2,3],[3,4]]
//Output: [-1,2,-1]
//Explanation: There is no right interval for [1,4] and [3,4].
//The right interval for [2,3] is [3,4] since start2 = 3 is the smallest start t
//hat is >= end1 = 3.
// 
//
// 
// Constraints: 
//
// 
// 1 <= intervals.length <= 2 * 104 
// intervals[i].length == 2 
// -106 <= starti <= endi <= 106 
// The start point of each interval is unique. 
// 
// Related Topics 二分查找 
// 👍 66 👎 0

package leetcode.editor.cn;

import java.util.Arrays;
import java.util.Comparator;

//java:Find Right Interval
public class P436FindRightInterval {
    public static void main(String[] args) {
        Solution solution = new P436FindRightInterval().new Solution();
    }

    class Solution {

        private int[][] leftBound2Index;

        public int[] findRightInterval(int[][] intervals) {
            if (intervals == null || intervals.length == 0 || intervals[0].length == 0)
                return new int[]{-1};
            this.leftBound2Index = new int[intervals.length][2];
            for (int i = 0; i < intervals.length; i++) {
                int[] interval = intervals[i];
                leftBound2Index[i][0] = interval[0];
                leftBound2Index[i][1] = i;
            }
            Arrays.sort(leftBound2Index, Comparator.comparingInt(o -> o[0]));
            int[] res = new int[intervals.length];
            for (int i = 0; i < intervals.length; i++) {
                int curRightBound = intervals[i][1];
                res[i] = findCeil(curRightBound);
            }
            return res;
        }

        private int findCeil(int val) {
            int l = 0, r = leftBound2Index.length - 1;
            while (l <= r) {
                int mid = (l + r) >> 1;
                int leftBound = leftBound2Index[mid][0];
                if (leftBound == val) {
                    return leftBound2Index[mid][1];
                } else if (leftBound < val) {
                    l = mid + 1;
                } else {
                    r = mid - 1;
                }
            }
            return l > leftBound2Index.length - 1 ? -1 : leftBound2Index[l][1];
        }
    }
}