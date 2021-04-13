``` c++
class Solution {
public:
    vector<int> findRightInterval(vector<vector<int>>& intervals) {
        int n = intervals.size();
        vector<int> ans(n, -1);
        unordered_map<int, int> um;
        for (int i = 0; i < n; ++i) {  //记录下每个区间原始位置
            um[intervals[i][0]] = i;
        }
        sort(intervals.begin(), intervals.end(), [&](const auto& v1, const auto& v2){  //按区间起点升序排序
            return v1[0] < v2[0];
        });
        for (int i = 0; i < n; ++i) {  //二分查找
            int target = intervals[i][1];
            int lo = i, hi = n - 1;
            while (lo <= hi) {
                int mi = lo + ((hi - lo) >> 1);
                if (intervals[mi][0] >= target) {
                    ans[um[intervals[i][0]]] = um[intervals[mi][0]];
                    hi = mi - 1;
                } else {
                    lo = mi + 1;
                }
            }
        }
        return ans;
    }
};
```
``` golang
type Interval struct {
	Start int
	End   int
}

func findRightInterval(intervals [][]int) []int {
	its := make([]Interval, 0)

	for i := 0; i < len(intervals); i++ {
		it := Interval{
			Start: intervals[i][0],
			End:   intervals[i][1],
		}
		its = append(its, it)
	}
	return findRightIntervalHelp(its)
}

func findRightIntervalHelp(intervals []Interval) []int {
	original := make(map[int]int)
	for i, _ := range intervals {
		original[intervals[i].Start] = i // 起始点，对应的原始索引
	}
	sort.Slice(intervals, func(i, j int) bool {
		return intervals[i].Start < intervals[j].Start
	}) // 按照左边界排序

	res := make([]int, len(intervals))

	for k, v := range intervals {
		lo := 0
		hi := len(intervals) - 1

		for lo < hi {
			mid := lo + (hi-lo)/2
			if intervals[mid].Start<v.End{
				lo=mid+1
			}else{
				hi = mid
			}
		}

		// 找到左边界，然后判断左边界是否合法
        // 左边界不等于当前索引
		if lo != k&& intervals[lo].Start >= v.End {
			res[original[intervals[k].Start]] = original[intervals[lo].Start]
		} else {
			res[original[intervals[k].Start]] = -1
		}
	}
	return res
}
```
