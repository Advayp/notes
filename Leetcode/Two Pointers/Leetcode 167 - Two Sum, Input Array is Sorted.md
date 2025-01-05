- **Problem Link**: https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/?envType=study-plan-v2&envId=top-interview-150


## My Solution
```python
class Solution(object):
    def twoSum(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype: List[int]
        """
        left = 0
        right = len(numbers) - 1

        while left < right:
            curr_sum = numbers[left] + numbers[right]

            if curr_sum > target:
                right -= 1
            elif curr_sum < target:
                left += 1
            else:
                return [left + 1, right + 1]

        return [-1, -1]
```

## Approach
- Leverage the fact that the input array is sorted
- Start left and right pointers at both ends of the array
- If the sum of the elements at both pointers is less than the target sum, we know we need to increase the sum. Since the array is sorted in non-decreasing order, this corresponds to increasing the left pointer by 1. 
- The converse applies too. If the sum is greater than the target sum, we decrement the right pointer.
- Once we reach the target sum, we return the position of the left and right pointers (we add one because the problem states the arrays are 1-indexed)
- If we can't find the target sum, we return `[-1, -1]` to indicate it wasn't found

**Category**: Two pointers


## Time and Space Complexity
- Time: `O(n)`
- Space: `O(1)`
## Similar Problems
- [[Leetcode/Leetcode]]