- Problem Link: https://leetcode.com/problems/triangle/description/?envType=problem-list-v2&envId=dynamic-programming

## My Solution
```python
class Solution:
	def minimumTotal(self, t):
		m = len(t[-1])
		
		dp = [[0]*(m+1) for _ in range(len(t)+1)]
		
		for i in range(len(t) - 1, -1, -1):
			for j in range(i, -1, -1):
				dp[i][j] = min(t[i][j] + dp[i+1][j], t[i][j] + dp[i+1][j+1])
	
		return dp[0][0]
```


## Approach
- Classic bottom-up dynamic programming problem
- Create a two dimensional array storing the minimum cost from that position to the end 
	- In code, this looks like `dp[i][j] = t[i][j] + min(dp[i+1][j], dp[i+1][j+1])`
	- `dp[i+1][j]` and `dp[i+1][j+1]` represent the two paths possible
	- You add the element in the triangular array to find the cost for a particular i, j
- This approach is $O(n^2)$ time and space
- It's possible to do this in $O(n)$ space and $O(n^2)$ time since you only need to store the $(i+1)^{th}$ array 

**Category**: Two-Dimensional Dynamic Programming

## Similar Problems
- [[Leetcode 322 - Coin Change]]
- [[Leetcode/Leetcode]]