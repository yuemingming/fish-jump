
``` go
func minimumSize(nums []int, maxOperations int) int {
    left := 1
    right := max(nums)
    var ans = 0
    for left <= right {
        y := (left + right) >> 1
        ops := 0
        for _,temp := range nums{
            ops = ops + (temp - 1) / y
        }
        if ops <= maxOperations{
            ans = y
            right = y - 1
        }else {
            left = y + 1
        }
    }
    return ans
}

func max(nums []int) int{
    ans := 0
    for _,temp :=  range nums{
        if(temp > ans){
            ans = temp
        }
    }
    return ans
}

```
