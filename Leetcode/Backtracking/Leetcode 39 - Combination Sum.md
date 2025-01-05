- **Problem Link**: https://leetcode.com/problems/combination-sum/description/


## My Solution
```python
class Solution(object):
    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        candidates.sort()
        res = []

        def backtrack(currentSum, combination, start):
            if currentSum == target:
                res.append(combination)
                return
            for i in range(start,len(candidates)):
                if currentSum+candidates[i]>target:
                    break
                combination = combination+[candidates[i]]
                backtrack(currentSum+candidates[i], combination, i)
                combination = combination[:-1]
        backtrack(0,[],0)
        return res
```

## Approach
- Sort candidates to ensure ascending order, allows for effective pruning later
- The structure of this solution is just like any recursive backtracking problem
- Output is a list of lists, so use one parameter to keep track of all valid combinations
- Base case is when the current sum equals the target, keep track of this in its own variable to prevent an unnecessary $O(n)$ operation
- Three steps:
	- Choose an element from the starting element onward, done by using a for loop starting at the current index and going till the end of the array
	- Explore: recursive call, update current sum, current candidates, and start index 
	- Unchoose: remove last element from combination, since lists are stored by reference
	- **Other notes:** If, based on the current sum, the current candidate we're checking exceeds the target, we can break due to the ascending order 

**Category**: Recursive Backtracking

## Similar Problems
- [[Leetcode 494 - Target Sum]]
- [[Leetcode/Leetcode]]