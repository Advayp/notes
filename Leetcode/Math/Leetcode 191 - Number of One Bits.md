- **Problem Link**:  https://leetcode.com/problems/number-of-1-bits/description/?envType=study-plan-v2&envId=top-interview-150


## My Solution
```python
class Solution(object):
    def hammingWeight(self, n):
        """
        :type n: int
        :rtype: int
        """
        res = 0
        while n != 0:
            res += n & 1
            n = n >> 1

        return res
```

## Approach
- Note that `n & 1` gives the value of the LSB.
- We can use this to our advantage by checking if the LSB is 1, adding to our total appropriately, and then shifting the bits of `n` to the right one bit.
- We continue this process until n is `0`, which means either there are no ones left or we've read and handled all the bits of `n`

**Category**: Math


## Time and Space Complexity
- Time: $O(n)$
- Space: $O(1)$
## Similar Problems
- [[Leetcode/Leetcode]]