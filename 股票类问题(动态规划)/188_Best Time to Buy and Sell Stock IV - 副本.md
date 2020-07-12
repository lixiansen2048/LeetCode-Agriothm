## 动态规划类
`d[i][k][0|1]`:第 i 天，最多允许进行 k 次交易，最多获得多少利益
[1]表示手上还持有股票，[0]表示手上没有股票

### 状态转移方程：
dp[i][k][0] = max(dp[i - 1][k][0], dp[i - 1][k][1] + price[i]) <br />
dp[i][k][1] = max(dp[i - 1][k][1], dp[i - 1][k - 1][0] - price[i])

```python
class Solution:
    def maxProfit(self, k: int, prices: List[int]) -> int:
        def maxProfit_k_inf(prices: List[int]) -> int:
            for i in range(n):
                if i == 0:
                    # dp[0][0] = 0
                    dp_0_0 = 0
                    # dp[0][1] = -prices[0]
                    dp_0_1 = -prices[0]
                else:
                    # dp[i][0] = max(dp[i - 1][0], dp[i - 1][1] + prices[i])
                    dp_0_0 = max(dp_0_0, dp_0_1 + prices[i])
                    # dp[i][1] = max(dp[i - 1][1], - prices[i])
                    dp_0_1 = max(dp_0_1, dp_0_0 - prices[i])

            return dp_0_0

        if prices == []:
            return 0

        n = len(prices)

        if k > n / 2:
            return maxProfit_k_inf(prices)

        dp = [[[0] * 2 for _ in range(k + 1)] for _ in range(n)]

        for i in range(n):
            for k in range(1,k+1):
                if i == 0:
                    # dp_0_10 = dp_0_20 = 0
                    # dp_0_11 = dp_0_21 = -prices[0]
                    dp[0][k][0] = 0
                    dp[0][k][1] = -prices[0]
                else:

                    dp[i][k][0] = max(dp[i - 1][k][0],dp[i - 1][k][1] + prices[i])
                    dp[i][k][1] = max(dp[i - 1][k][1],dp[i - 1][k - 1][0] - prices[i])


        return dp[n - 1][k][0]
```