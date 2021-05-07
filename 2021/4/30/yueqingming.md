class Solution {
    public int smallestDivisor(int[] nums, int threshold) {
        int left = 1;
        // int right = nums[nums.length-1];     // 当nums数组是有序, nums数组中最大值是最后一位
        int right = Integer.MIN_VALUE;          // 当nums数组是无序, 扫描查找最大值
        for (int num: nums) {
            right = Math.max(right, num);
        }
        // PS: 面试找最大值不要使用Collections.max(), 别问我是怎么知道的
        
        // 注意循环条件, 如果循环条件为(left < right), left和right重叠时会跳出循环
        while (left <= right) {
            // 计算mid, 小心溢出
            // int mid = (left + right) / 2;               // 方法一  会溢出
            // int mid = left + (right - left) / 2;     // 方法二  无溢出
            int mid = left + ((right - left) >> 1);    // 方法三  无溢出

            int sum = findDivisor(nums, mid);

            if (sum > threshold) {
                left = mid + 1;         // 右区间 (mid, right]
            } else {
                right = mid - 1;        // 左区间 [left, mid)
            }
        }
        return left;
    }

    public int findDivisor(int[] nums, int divisor) {
        int sum = 0;
        for (int num: nums) {
            sum += (num / divisor) + (num % divisor == 0 ? 0 : 1);
        }
        return sum;
    }
}

