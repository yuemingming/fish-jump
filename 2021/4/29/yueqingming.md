/*
 * // This is the custom function interface.
 * // You should not implement it, or speculate about its implementation
 * class CustomFunction {
 *     // Returns f(x, y) for any given positive integers x and y.
 *     // Note that f(x, y) is increasing with respect to both x and y.
 *     // i.e. f(x, y) < f(x + 1, y), f(x, y) < f(x, y + 1)
 *     public int f(int x, int y);
 * };
 */
class Solution {
    public List<List<Integer>> findSolution(CustomFunction customfunction, int z) {
        List<List<Integer>> res = new ArrayList<>();
        //定义x为i
        for (int i = 1; i <= 1000; i++) {
            if (customfunction.f(i,1) > z) {
                break;
            }
            int left = 1;
            int right = 1000;
        //在一到1000里查找这个数,有的话就添加并且break
            while (left <= right) {
                int mid = (right + left) / 2;
                int temp = customfunction.f(i,mid);
                if (temp == z) {
                    List<Integer> list = new ArrayList<>();
                    list.add(i);
                    list.add(mid);
                    res.add(list);
                    break;
                } else if (temp > z) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            }
        }
        return res;
    }
}

