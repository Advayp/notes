- **Problem Link**: https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/?envType=study-plan-v2&envId=top-interview-150


## My Solution
```python
class Solution(object):
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        combs = {
            "2": "abc",
            "3": "def",
            "4": "ghi",
            "5": "jkl",
            "6": "mno",
            "7": "pqrs",
            "8": "tuv",
            "9": "wxyz"
        }

        def helper(digits, curr, ret=[]):
            if len(digits) == 0:
                if curr:
                    ret.append(curr)
                return

            choice = digits[0]

            for i in range(len(combs[choice])):
                helper(digits[1:], curr + combs[choice][i], ret)

        ret = []
        helper(digits, "", ret)
        return ret
        
```

## Approach
- Standard recursive backtracking problem
- Choose one letter from the list of available letters for each digit 
- Explore by adding it to the current string and repeating the "choice" step for the other digits
	- Once we run out of digits to make a choice from, add the current combination to the list containing all combinations 
- Unchoose the current letter by moving on to the next letter in a digit's available letters


**Category**: Recursive Backtracking


## Time and Space Complexity
- Time: $O(nd)$
	- Where `d` is the length of the list of possible letters a digit can represent
- Space: $O(1)$
	- Excluding stack space
## Similar Problems
- [[Leetcode 39 - Combination Sum]]
- [[Leetcode 494 - Target Sum]]