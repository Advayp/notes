- **Problem Link**: https://leetcode.com/problems/coin-change/description/?envType=problem-list-v2&envId=dynamic-programming

## My Solution
```python
class Solution(object):
	def coinChange(self, coins, amount):
		"""
		:type coins: List[int]
		:type amount: int
		:rtype: int
		"""
	
		dp = [(amount+1)] * (amount + 1)
		
		dp[amount] = 0
		
		for i in range(amount-1, -1, -1):
			for c in coins:
				if i + c <= amount:
					dp[i] = min(dp[i], dp[i+c] + 1)
		
		return dp[0] if dp[0] != amount + 1 else -1
```


## Approach
- Create a one-dimensional array with index `i` storing the minimum number of coins needed to have `i` money
- For every single possible coin, compute the minimum coins by using `dp[i+c] + 1`
	- `dp[i+c]` is the number of coins needed to make `i+c` amount
	- `+1` to count the currently used coin
- Time complexity: $O(nc)$
	- $c$ is the number of coins
- Space complexity: $O(n)$

**Category**: One Dimensional Dynamic Programming
## Similar Problems
- [[Leetcode 120 - Triangle]]
- [[Leetcode/Leetcode]]