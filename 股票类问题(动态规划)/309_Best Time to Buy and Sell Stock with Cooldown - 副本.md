## 动态规划类
`d[i][k][0|1]`:第 i 天，最多允许进行 k 次交易，最多获得多少利益
[1]表示手上还持有股票，[0]表示手上没有股票

### 状态转移方程：
dp[i][k][0] = max(dp[i - 1][k][0], dp[i - 1][k][1] + price[i]) <br />
dp[i][k][1] = max(dp[i - 1][k][1], dp[i - 1][k - 1][0] - price[i])

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if prices == []:
            return 0

        n = len(prices)
        dp = [[0] * 2 for _ in range(n)]

        for i in range(len(prices)):
            if i == 0:

                # dp_0_0 = 0
                # dp_0_1 = -prices[0]
                dp[0][1] = -prices[0]
                dp[0][0] = 0
            elif i == 1:
                dp[i][0] = max(dp[i - 1][0], dp[i - 1][1] + prices[i])
                dp[i][1] = max(dp[i - 1][1], - prices[i])
            else:
                dp[i][0] = max(dp[i - 1][0], dp[i - 1][1] + prices[i])
                dp[i][1] = max(dp[i - 1][1], dp[i - 2][0] - prices[i])


        return dp[n - 1][0]
```