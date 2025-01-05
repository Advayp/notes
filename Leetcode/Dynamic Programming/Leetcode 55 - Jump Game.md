- **Problem Link**: https://leetcode.com/problems/jump-game/description/?envType=problem-list-v2&envId=dynamic-programming


## My Solution
```python
class Solution(object):
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        target = len(nums) - 1

        for i in range(len(nums) - 2, -1, -1):
            if i + nums[i] >= target:
                target = i
        
        return target == 0
        
```

## Approach
- Construct an array with length `n`  in which each index `i` stores whether or not it is possible to reach the end of the array from that index
- Initialize this array to contain `False`
- Use bottom-up dynamic programming in the following way:
	- Set `dp[n - 1] = True`, since we've reached the end
	- Set `dp[i] = i + nums[i] > n - 1 or dp[i + nums[i]]`
	- First part checks if we can jump past the end, in which case we know we can reach the end from index `i`
	- Second part checks if the max index we jump to can reach the end
		- When actually implementing this, you would have to check all jumps in the range $[0, n_i - 1]$ 
	- This approach overall has time complexity $O(n^2)$ and space complexity $O(n)$
- To avoid this, we can use the above implementation

**Category**: One dimensional dynamic programming

## Similar Problems
- [[Leetcode 322 - Coin Change]]
- [[Leetcode 120 - Triangle]]
- [[Leetcode/Leetcode]]