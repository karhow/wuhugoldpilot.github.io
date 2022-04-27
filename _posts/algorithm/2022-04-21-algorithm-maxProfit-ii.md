---
layout: article
title: 买卖股票的最佳时机 II
tags: algorithm greedy 
sharing: true
show_author_profile: true
typora-copy-images-to: ..\..\assets\blog_img
typora-root-url: ..\..
key: 2022-04-21-algorithm-maxProfit-ii
comment: true
mermaid: true
chart: true
---

# 题目描述

给你一个整数数组prices，其中prices[i]表示某支股票第i天的价格。在每一天，你可以决定是否购买和/或出售股票。你在任何时候最多只能持有一股股票。你也可以先购买，然后在同一天出售。返回你能获得的最大利润。

示例 1：  
输入：prices = [7,1,5,3,6,4]  
输出：7  
解释：在第2天（股票价格=1）的时候买入，在第3天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润=5-1=4。随后，在第4天（股票价格=3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润=6-3=3。总利润为4 + 3= 7.   

示例 2：   
输入：prices = [1,2,3,4,5]  
输出：4  
解释：在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5 - 1 = 4。总利润为 4 。  

示例 3：   
输入：prices = [7,6,4,3,1]  
输出：0  
解释：在这种情况下, 交易无法获得正利润，所以不参与交易可以获得最大利润，最大利润为 0 。  
 
提示：
$1 <= prices.length <= 3*10^4$  
$0 <= prices[i] <= 10^4$

# 解题思路

## 贪心解法

由于股票购买没有限制，我们可以在同一天买入卖出，这样就等价与寻找x个长度为1的使利益最大化的数组。从贪心的角度来考虑就是每次选择大于0的profit就可以使利益最大化，需要注意的是贪心算法只是用来计算最大利益，并**不等于实际的交易过程**。就如题目中例子prices = [1,2,3,4,5]，我们计算的时候是前一天买入当前卖出，然后再当天买入，等明天卖出。从实际交易来说我们并不会进行4次买入4次卖出这样的操作；我们只会第一天买入，第五天卖出。但是从计算最大收益的角度来说，采用这样的贪心策略算出的利益是最大的。

# 代码

golang实现：
```go
func maxProfit(prices []int) (ans int) {
	n := len(prices)
	for i := 1; i < n; i++ {
		ans += max(0, prices[i]-prices[i-1])
	}
	return
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
```

# 时间和空间复杂度

- 时间复杂度：$O(n)$，其中 $n$ 是数组的长度。需要遍历数组1次。
- 空间复杂度：$O(1)$，需要常数空间存放变量。