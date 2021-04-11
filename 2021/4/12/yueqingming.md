> 将数组分为A,B 和 C,D 两组，分别遍历两个集合得出相加和的枚举，然后判断是否包含相反数的和
``` golang
func fourSumCount(a, b, c, d []int) (ans int) {
    countAB := map[int]int{}
    for _, v := range a {
        for _, w := range b {
            countAB[v+w]++
        }
    }
    for _, v := range c {
        for _, w := range d {
            ans += countAB[-v-w]
        }
    }
    return
}
```
