**暴力贪心**
``` golang
func findRadius(houses []int, heaters []int) int {
    sort.Ints(houses)
    sort.Ints(heaters)
    var res int = 0
    for _,house := range houses{
        var i int = 0
        for i + 1 < len(heaters) && abs(heaters[i] - house) >= abs(heaters[i + 1] - house){
            i++
        }
        res = max(res,abs(heaters[i] - house))
    }
    return res
}

func abs(num int) int{
    if num > 0{
        return num
    }else{
        return -num
    }
}
func max(a int, b int) int{
    if(a > b){
        return a
    }else{
        return b
    }
}
```
**二分查找**
``` java
class Solution {
    public int findRadius(int[] houses, int[] heaters) {
        Arrays.sort(houses);
        Arrays.sort(heaters);
        int res = 0;
        for (int house : houses) {
            // 二分查找
            int l = 0;
            int r = heaters.length - 1;
            // 在heaters中找到最接近house的左侧的值
            while (l < r) {
                int mid = l + r >> 1;
                if (heaters[mid] >= house) r = mid;
                else l = mid + 1;
            }
            int leftTmp = l;
            l = 0;
            r = heaters.length - 1;
            // 在heaters中找到最接近house的左侧的值
            while (l < r) {
                int mid = l + r + 1>> 1;
                if (heaters[mid] <= house) l = mid;
                else r = mid - 1;
            }

            int rightTmp = r;
            // 左右侧值取最小的，结果取所有最小中的最大的
            res = Math.max(res, Math.min(Math.abs(heaters[leftTmp] - house), Math.abs(heaters[rightTmp] - house)));
        }

        return res;
    }
}
```

