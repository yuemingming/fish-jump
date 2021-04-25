public class P74SearchA2dMatrix {
    public static void main(String[] args) {
        Solution solution = new P74SearchA2dMatrix().new Solution();
    }

    class Solution {
        public boolean searchMatrix(int[][] matrix, int target) {
            int i = matrix.length - 1, j = 0;
            while (i >= 0 && j < matrix[0].length) {
                int curVal = matrix[i][j];
                if (curVal == target) return true;
                if (curVal < target) {
                    j ++;
                } else {
                    i --;
                }
            }
            return false;
        }
    }
}