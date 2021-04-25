暴力解法的过程中，我们发现最坏情况下对于任意 i 与 j ，A[i] 与 B[j] 比较了 \min(i + 1, j + 1)min(i+1,j+1) 次。这也是导致了该暴力解法时间复杂度过高的根本原因。

不妨设 A 数组为 [1, 2, 3]，B 两数组为为 [1, 2, 4] ，那么在暴力解法中 A[2] 与 B[2] 被比较了三次。这三次比较分别是我们计算 A[0:] 与 B[0:] 最长公共前缀、 A[1:] 与 B[1:] 最长公共前缀以及 A[2:] 与 B[2:] 最长公共前缀时产生的。

我们希望优化这一过程，使得任意一对 A[i] 和 B[j] 都只被比较一次。这样我们自然而然想到利用这一次的比较结果。如果 A[i] == B[j]，那么我们知道 A[i:] 与 B[j:] 的最长公共前缀为 A[i + 1:] 与 B[j + 1:] 的最长公共前缀的长度加一，否则我们知道 A[i:] 与 B[j:] 的最长公共前缀为零。

这样我们就可以提出动态规划的解法：令 dp[i][j] 表示 A[i:] 和 B[j:] 的最长公共前缀，那么答案即为所有 dp[i][j] 中的最大值。如果 A[i] == B[j]，那么 dp[i][j] = dp[i + 1][j + 1] + 1，否则 dp[i][j] = 0。

这里借用了 Python 表示数组的方法，A[i:] 表示数组 A 中索引 i 到数组末尾的范围对应的子数组。

考虑到这里 dp[i][j] 的值从 dp[i + 1][j + 1] 转移得到，所以我们需要倒过来，首先计算 dp[len(A) - 1][len(B) - 1]，最后计算 dp[0][0]。
因为此处只关心 i + 1,以及 i 两个状态，所以可以做状态压缩。
``` golang
func findLength(A []int, B []int) int {
    n, m := len(A), len(B)
    dp := make([][]int, 2)
    for i := 0; i < 2; i++{
        dp[i] = make([]int,m + 1)
    }
    ans := 0
    for i := n - 1; i >= 0; i-- {
        for j := m - 1; j >= 0; j-- {
            if A[i] == B[j] {
                dp[i % 2][j] = dp[(i + 1) % 2][j + 1] + 1
            } else {
                dp[i % 2][j] = 0
            }
            if ans < dp[i % 2][j] {
                ans = dp[i % 2][j]
            }
        }
    }
    return ans
}
```
``` golang
const (
    base, mod = 113, 1000000009
)

func findLength(A []int, B []int) int {
    check := func(length int) bool {
        hashA := 0
        for i := 0; i < length; i++ {
            hashA = (hashA * base + A[i]) % mod
        }
        bucketA := map[int]bool{hashA: true}
        mult := qPow(base, length - 1)
        for i := length; i < len(A); i++ {
            hashA = ((hashA - A[i - length] * mult % mod + mod) % mod * base + A[i]) % mod
            bucketA[hashA] = true
        }

        hashB := 0
        for i := 0; i < length; i++ {
            hashB = (hashB * base + B[i]) % mod
        }
        if bucketA[hashB] {
            return true
        }
        for i := length; i < len(B); i++ {
            hashB = ((hashB - B[i - length] * mult % mod + mod) % mod * base + B[i]) % mod
            if bucketA[hashB] {
                return true
            }
        }
        return false
    }

    left, right := 1, min(len(A), len(B)) + 1
    for left < right {
        mid := (left + right) >> 1
        if check(mid) {
            left = mid + 1
        } else {
            right = mid
        }
    }
    return left - 1
}

func qPow(x, n int) int {
    ret := 1
    for n != 0 {
        if n & 1 != 0 {
            ret = ret * x % mod
        }
        x = x * x % mod
        n >>= 1
    }
    return ret
}

func min(x, y int) int {
    if x < y {
        return x
    }
    return y
}
```
二分查找将某个子序列整体作为一个值，使用 Hash + 二分查找。
