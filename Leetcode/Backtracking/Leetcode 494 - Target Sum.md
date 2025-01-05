- **Problem Link**: https://leetcode.com/problems/target-sum/?envType=problem-list-v2&envId=dynamic-programming

## My Solution
```python
class Solution(object):

	def findTargetSumWays(self, nums, target):
	
		"""
		:type nums: List[int]
		
		:type target: int

		:rtype: int
		
		"""
	
		dp = {} # (index, val), done to cache and speed up the process
	
		def backtrack(i, total):
			if i == len(nums):
				return 1 if total == target else 0
			
			if (i, total) in dp:
				return dp[(i, total)]
			
			dp[(i, total)] = backtrack(i + 1, total + nums[i]) + backtrack(i + 1, total - nums[i])
			
			  
			return dp[(i, total)]
	
	
		return backtrack(0, 0)
```

## Approach
- Basic backtracking question 
- If at the end of the array:
	- Return 1 if the total matches that provided, 0 if not
- Two choices:
	- Add the current value to the total
	- Subtract the current value from the total
- In code, these look like the following respectively:
	- `backtrack(i + 1, total + nums[i])`
	- `backtrack(i + 1, total - nums[i])`
- Caching makes this solution $O(n)$ instead of $O(2^n)$

**Category**: Recursion/Backtracking

## Similar Problems
- [[Leetcode 39 - Combination Sum]]
- [[Leetcode/Leetcode]]