class Solution {
    public int[] maxDepthAfterSplit(String seq) {
        int d = 0;
        int length = seq.length();
        int[] ans = new int[length];
        for (int i = 0; i < length; i++) {
            if (seq.charAt(i) == '(') {
                ++d;
                ans[i] = d % 2;
            } else {
                ans[i] = d % 2;
                --d;
            }
        }
        return ans;
    }
}
