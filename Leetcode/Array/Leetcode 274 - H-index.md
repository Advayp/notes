- **Problem Link**: https://leetcode.com/problems/h-index/description/


## My Solution
```python
class Solution:
    def hIndex(self, citations):
        n = len(citations)
        citations.sort()

        for i,v in enumerate(citations):
            if n - i <= v:
                return n - i
                
        return 0
```

## Approach
- H-index is defined as the maximum value of `h` such that a given research has published at least `h` papers that have been cited at least `h` times
- Sort the array to ensure it's easy to find the number of papers that have cited at least `citations[i]` times. This is simply given by `len(citations) - i`
- Thus, the problem is related to maximizing the value of `len(citations) - i`
- However, to meet the requirements of the h-index, `len(citations) - i` must be less than `citations[i]`. We return the first instance of this since `len(citations) - i` decreases as `i` increases

**Category**: Arrays


## Time and Space Complexity
- Time: $O(n)$
- Space: $O(1)$
## Similar Problems
- [[Leetcode/Leetcode]]