//Given two integer arrays nums1 and nums2, return an array of their intersectio
//n. Each element in the result must be unique and you may return the result in an
//y order. 
//
// 
// Example 1: 
//
// 
//Input: nums1 = [1,2,2,1], nums2 = [2,2]
//Output: [2]
// 
//
// Example 2: 
//
// 
//Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
//Output: [9,4]
//Explanation: [4,9] is also accepted.
// 
//
// 
// Constraints: 
//
// 
// 1 <= nums1.length, nums2.length <= 1000 
// 0 <= nums1[i], nums2[i] <= 1000 
// 
// Related Topics 排序 哈希表 双指针 二分查找 
// 👍 352 👎 0

package leetcode.editor.cn;

import java.util.HashSet;
import java.util.Iterator;
import java.util.Set;

//java:Intersection of Two Arrays
public class P349IntersectionOfTwoArrays {
    public static void main(String[] args) {
        Solution solution = new P349IntersectionOfTwoArrays().new Solution();
    }

    class Solution {
        public int[] intersection(int[] nums1, int[] nums2) {
            Set<Integer> nums1Set = new HashSet<>();
            for (int num : nums1) nums1Set.add(num);
            Set<Integer> res = new HashSet<>();
            for (int num : nums2) {
                if (nums1Set.contains(num)) {
                    res.add(num);
                }
            }
            Iterator<Integer> resIt = res.iterator();
            int index = 0;
            int[] intersection = new int[res.size()];
            while (resIt.hasNext()) intersection[index++] = resIt.next();
            return intersection;
        }
    }
}