## 动态规划类
`d[i][k][0|1]`:第 i 天，最多允许进行 k 次交易，最多获得多少利益
[1]表示手上还持有股票，[0]表示手上没有股票

### 状态转移方程：
dp[i][k][0] = max(dp[i - 1][k][0], dp[i - 1][k][1] + price[i]) <br />
dp[i][k][1] = max(dp[i - 1][k][1], dp[i - 1][k - 1][0] - price[i])

```python
class Solution:
    def maxProfit(self, prices: List[int], fee: int) -> int:

        if prices == []:
            return 0

        for i in range(len(prices)):
            if i == 0:
                d_0_0 = 0
                d_0_1 = -prices[0] - fee
            else:

                d_0_0 = max(d_0_0,d_0_1 + prices[i])
                d_0_1 = max(d_0_1,d_0_0 - prices[i] - fee)

        return d_0_0
```