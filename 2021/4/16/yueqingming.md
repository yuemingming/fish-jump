``` golang
func minEatingSpeed(piles []int, h int) int {
    lo,hi := 1,1000000000
    for lo < hi {
        mi := lo + ((hi - lo) >> 1)
        if !possible(piles,h,mi){
            lo = mi + 1
        }else{
            hi = mi
        }
    }
    return lo
}

func possible(piles []int,H int, K int) bool {
    time := 0
    for _,p := range piles{
        time += (p -1) / K + 1
    }
    return time <= H
}

```
