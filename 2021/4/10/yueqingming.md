二分解法

> n + 1 个数的取值范围为 1 - n,那么必定有数字出现了两次及以上，通过二分排查看每个区间出现数值次数就能每次排除一半范围。
``` go
func findDuplicate(nums []int) int {

    left,right := 1, len(nums) - 1
    for left < right {
        mid := left + ((right - left) >> 1)
        count := 0
        for _,num := range nums{
            if left <= num && num <= mid{
                count = count + 1
            }
        }
        if count > mid - left + 1{
            right = mid
        }else{
            left = mid + 1
        }

    }
 return left
}
```
### 快慢指针

> 每个 index 位置对应的数即代表当前节点指向的下一个节点，如果存在重复的数就会形成环，通过快慢指针可以判断是否存在环。

证明为什么会走到L
假设入环之前的长度为L, 入环之后快慢指针第一相遇时快指针比慢指针🐢多跑了N圈, 每一圈的长度为C, 此时快指针🐰在环内离入环节点的距离为C'
此时慢指针🐢走过的距离为: L + C'
此时快指针🐰走过的距离为: L + C' + N * C
因为快指针🐰的速度是慢指针🐢的两倍, 所以有: 2 * (L + C') = L + C' + N * C
整理后得到: (N - 1) * C + (C - C') = L
由此可知, 若此时有两个慢指针🐢同时分别从链表头结点和快慢指针第一次相遇的节点出发, 两者必然会在入环节点相遇

L + C' + L = L + C' + (N - 1) * C + C - C' = L + N * C
从而得出会在入口处相遇
