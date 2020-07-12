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

        for i in range(n):
            if i == 0:
                dp_0_10 = dp_0_20 = 0
                dp_0_11 = dp_0_21 = -prices[0]
            else:
                dp_0_10 = max(dp_0_10,dp_0_11 + prices[i])
                dp_0_20 = max(dp_0_20,dp_0_21 + prices[i])

                dp_0_11 = max(dp_0_11,-prices[i])
                dp_0_21 = max(dp_0_21,dp_0_10-prices[i])

        return dp_0_20
```