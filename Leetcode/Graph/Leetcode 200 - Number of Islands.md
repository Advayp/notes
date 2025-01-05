- **Problem Link**: https://leetcode.com/problems/number-of-islands/?envType=study-plan-v2&envId=top-interview-150


## My Solution
```python
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """

        def bfs(grid, i, j):
            if (i < 0 or i >= len(grid) or j < 0 or j >= len(grid[i]) or grid[i][j] == '0'): return

            grid[i][j] = "0"
            bfs(grid, i + 1, j)
            bfs(grid, i - 1, j)
            bfs(grid, i, j + 1)
            bfs(grid, i, j - 1)


        count = 0

        for i in range(len(grid)):
            for j in range(len(grid[i])):
                if grid[i][j] == "1":
                    count += 1
                    bfs(grid, i, j)

        return count
        

```

## Approach
- Standard BFS Problem
- Loop over each cell in the grid 
- If the cell contains the value 1:
	- Increment the total count by 1 
	- Set all connected 1s to 0 (to avoid searching for them again) by using BFS
  
**Category**: Graph 


## Time and Space Complexity
- Time: $O(m^2 n^2)$
- Space:  $O(1)$
## Similar Problems
- [[Leetcode 399 - Evaluate Division]]
- [[Leetcode/Leetcode]]