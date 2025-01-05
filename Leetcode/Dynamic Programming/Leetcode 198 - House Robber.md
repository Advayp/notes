- **Problem Link**: https://leetcode.com/problems/house-robber/?envType=study-plan-v2&envId=top-interview-150


## My Solution
```python
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        dp = [0] * (len(nums) + 2)
        for i in range(len(nums) - 1, -1, -1):
            dp[i] = max(dp[i + 1], nums[i] + dp[i + 2])
        return dp[0] 

```

## Approach
- Dynamic programming question
- `dp[i]` stores the maximum amount that can be robbed starting at index `i`
- At each index `i`, we have two options
	- Steal from the current index (`nums[i]`) and advance 
		- Since we can't steal from the adjacent one we go to the house two houses after `dp[i + 2]`
	- Ignore the current one and steal from the next one `dp[i + 1]`
	- Store the max values from these in `dp[i]`


**Category**: Dynamic Programming


## Time and Space Complexity
- Time: $O(n)$
- Space:  $O(n)$
## Similar Problems
- [[Leetcode/Leetcode]]
- - [[Leetcode 322 - Coin Change]]
- [[Leetcode 120 - Triangle]]
- [[Leetcode 55 - Jump Game]]
- [[Leetcode 45 - Jump Game II]]