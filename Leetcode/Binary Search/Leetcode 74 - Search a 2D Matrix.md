- **Problem Link**: https://leetcode.com/problems/search-a-2d-matrix/description/


## My Solution
```python
class Solution(object):
    
    def searchMatrix(self, matrix, target):
        
        def total_units(pos):
            return pos[0] * len(matrix[0]) + pos[1]
        
        def find_mid(left, right):
            mid = left[::]
            diff = total_units(right) - total_units(left)
            mid[1] += diff // 2   
            mid[0] += mid[1] // len(matrix[0])
            mid[1] = mid[1] % len(matrix[0])
            return mid

        left = [0, 0]
        right = [len(matrix) - 1, len(matrix[0]) - 1]
        
        while True:
            mid = find_mid(left, right)
            val = matrix[mid[0]][mid[1]]
            if total_units(left) >= total_units(right) or left == mid:
                break
            
            if val == target:
                return True
            elif val < target:
                left = mid
            else:
                right = mid
            
        
        return matrix[left[0]][left[1]] == target or matrix[right[0]][right[1]] == target
```

## Approach
- Need new way of computing the middle element and deciding when `left > right` (the trivial case in binary search) 
- This is done by using a "unit" system, where the 2D array is effectively transformed into a 1D array 
- The basic principles of binary search follow after the above is implemented properly

**Category**: Binary Search


## Time and Space Complexity
- Time: $O(\log{m} * \log{n})$
- Space: $O(1)$
## Similar Problems
- [[Leetcode/Leetcode]]
