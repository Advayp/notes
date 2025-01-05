- **Problem Link**: https://leetcode.com/problems/minimum-cost-to-convert-string-i/


## My Solution
```python
from collections import defaultdict
from heapq import heappush, heappop


class Solution:
    def minimumCost(self, source, target, original, changed, cost):

        n = len(source)

        # create graph from given information
        adj = defaultdict(list)

        for src, dest, cost in zip(original, changed, cost):
            adj[src].append((cost, dest))

        # dijkstra's algorithm
        def dijkstra(src):
            heap = [(0, src)]

            min_cost_heap = {}

            while heap:
                cost, node = heappop(heap)
                if node in min_cost_heap:
                    continue
                min_cost_heap[node] = cost
                for nei_cost, nei in adj[node]:
                    heappush(heap, (cost + nei_cost, nei))

            return min_cost_heap

        min_costs = {c: dijkstra(c) for c in set(source)}

        total = 0

        for src, dest in zip(source, target):
            if not dest in min_costs[src]:
                return -1

            total += min_costs[src][dest]

        return total

```

## Approach
- This is a graph problem and involves repeatedly using Dijkstra's algorithm to find the minimum cost to convert one string to another 
- First step: create an adjacency matrix with the weight of the edge between two nodes being the given cost 
- Next, for each character in the source list, use Dijkstra's algorithm to create a map containing the minimum cost to travel to a particular node
- Lastly, loop over the source and target strings and check if it's possible to convert from the current source character to the current target character
	- If it is, add the cost to the total cost
	- If it's not, return `-1` (as per the instructions of the problem)
 
**Category**: Graph

## Time and Space Complexity
- Time: $O(n^2)$
- Space: $O(n)$
## Similar Problems
- [[Leetcode 399 - Evaluate Division]]
- [[Leetcode 200 - Number of Islands]]
- [[Leetcode/Leetcode]]