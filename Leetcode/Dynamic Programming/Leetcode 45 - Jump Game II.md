- **Problem Link**: https://leetcode.com/problems/jump-game-ii/description/?envType=problem-list-v2&envId=dynamic-programming


## My Solution
```python
class Solution(object):
    def jump(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        dp = [float('inf') for j in range(len(nums))]

        dp[len(nums) - 1] = 0

        for i in range(len(nums) - 2, -1, -1):
            for j in range(nums[i], 0, -1):
                if i + j >= len(nums) - 1:
                    dp[i] = 1
                    break
                dp[i] = min(dp[i], 1 + dp[i+j])

        return dp[0]
        
```

## Approach
- Bottom-up dynamic programming
- Initialize an array of length `n` with each entry set to infinity. At each index i, the array stores the minimum number of steps from i to the end
- If we can jump from the current index directly to the end, we can set `dp[i] = 1` and move on, since this is the minimum possible case
- If not, loop over the possible options ($[1, n_i]$) and do the following:
	- Compute the minimum number of steps after this move (which is stored in `dp[i + j]` due to bottom-up dynamic programming) 
		- Make sure to add 1 since we're jumping
	- Store the minimum number in `dp[i]` each iteration

**Category:** Two dimensional dynamic programming

## Time and Space Complexity
- Time: $O(n)$
- Space: $O(n)$

## Similar Problems
- [[Leetcode 120 - Triangle]]
- [[Leetcode 55 - Jump Game]]
- [[Leetcode 322 - Coin Change]]
- [[Leetcode/Leetcode]]
