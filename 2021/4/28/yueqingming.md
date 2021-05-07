class Solution {
   /**
     * 思路：遍历 + 记忆化 + 前缀和。这题解是直接给出了多重优化后的思路，在写的时候一遍一遍的思考出更优的方式
     *
     * 公共方法：find(String str) 用来查询这个字符串最小的字符出现的次数
     * 方式一：暴力，就是拿queries的每个元素，去对比words的每个元素，满足条件的记录下来，这里每次都调find
     *      那就存在问题：words每个元素每次比较都调find，浪费了，可以每次调了之后，记录这个元素对应的find结果，所以有了方式二
     *
     * 方式二：在方式一的基础上，我们用一个和words等长的int类型数组record，记录words每个元素计算后的find结果，供后面使用
     *       这种方式存在性能问题就是：queries每个元素要一一对比record所有元素，还是双重循环，性能不够
     *
     * 方式三：在方式二的基础上，根据题目条件，words每个元素长度不会超过10，那也就是words元素每个find值只可能为1和10之间，那
     *       这时候我们可以用大小11的int类型数组record记录words中所有元素的find结果里，每种find结果对应出现的次数，数组下标为出现的次数
     *       这样那queries的每个元素find结果，从record数组后往前找，小于的下标就不用继续了，直接提前结束。
     *
     * 方式四：方式三还是需要从尾开始遍历record，这种求数组连续子数组和的问题，可以立马先到 前缀和，这样就可以直接通过下标将数组值相减
     *       就可以得到结果了！这也就是最终的方案
     */
    public int[] numSmallerByFrequency(String[] queries, String[] words) {
        int queriesLen = queries.length;
        int wordsLen = words.length;

        // 记录words里面的每个的个数,这里题目说了，给出每个字符串长度在1到10之间
        // 所以用一个大小等于11的，就可以记录每个数出现的次数，这就类似 基数排序
        // 这样对每个queries[i]，获得其个数后，只要判断即可
        int[] record = new int[11];
        int[] result = new int[queriesLen];

        int count;
        for (int i = 0; i < wordsLen; i++){
            count = find(words[i]);
            record[count] += 1;
        }

        for (int i = 1; i < 11; i++){ // 前缀和
            record[i] = record[i] + record[i-1];
        }

        int curQueryCount;
        for (int i = 0; i < queriesLen; i++){
            curQueryCount = find(queries[i]);

            result[i] = record[10] - record[curQueryCount];
        }

        return result;
    }

    public int find(String str){
        char curMinChar = 'z';
        int curMinCharCount = 0;

        for (int i = 0; i < str.length(); i++){
            if (str.charAt(i) == curMinChar){
                curMinCharCount++;
            }else if (str.charAt(i) < curMinChar){ // 出现更小的，则更新记录
                curMinChar = str.charAt(i);
                curMinCharCount = 1;
            }
        }

        return curMinCharCount;
    }

}
