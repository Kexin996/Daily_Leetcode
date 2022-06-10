# 714. Best Time to Buy and Sell Stock with Transaction Fee

[https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

```java
class Solution {
    public int maxProfit(int[] prices, int fee) 
    {
        // Greedy
        int min = prices[0];
        int sum = 0;
        for (int p: prices)
        {
            // 为什么p 《 min:
            // [1,3,2]:
            // 如果没有这个条件，我们所取的就不是最小的min
            // p比我们目前的min还小，说明该买入了
            if (p < min && p < min+fee)
            {
                min = p;
            }
            // 我们实际上是买入了这个股票握在手里，
            // 在遇到if满足的时候才卖
            // 但如果跑完了loop就说明我们在这个p卖掉了
            else if (p > min+fee)
            {
                sum += p-min-fee;
                // 因为是持有/也可以算卖掉，而且我们count了净利润，这个
                // min是要减掉fee的，因为我们在if statement里面是没算
                // transaction fee
                
                // 这个时候其实我们就是要找比这个小的p接盘
                min = p-fee;
            }
        }
        return sum;
        }
    }
}
```

* 这道题一开始加了 fee，是因为交易一次收fee可以在结尾收，也可以在开头收。我们直接假定1是最小的价格开始收钱。
* 如果 p+fee < res:
  * 该买入了，也就是说我们卖掉了之前持有的股票
* 如果 p > res:
  *
