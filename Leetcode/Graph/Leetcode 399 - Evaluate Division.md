- **Problem Link**: https://leetcode.com/problems/evaluate-division/description/?envType=study-plan-v2&envId=top-interview-150


## My Solution
```python
class Solution(object):
    def calcEquation(self, equations, values, queries):
        """
        :type equations: List[List[str]]
        :type values: List[float]
        :type queries: List[List[str]]
        :rtype: List[float]
        """
        
        adj = defaultdict(list)
        for (start, end), value in zip(equations, values):
            adj[start].append((value, end))
            adj[end].append((1.0/value, start))

        def create_map(node):
            # weight, node
            h = [(1, node)]
            res = {}

            while h:
                weight, current_node = h.pop()
                if current_node in res:
                    continue
                res[current_node] = weight
                for edge_weight, dest in adj[current_node]:
                    h.append((weight * edge_weight, dest))

            return res

        maps = {c: create_map(c) for c in adj}

        result = []

        for src, dest in queries:
            if src not in maps or dest not in maps[src]:
                result.append(-1)
            else:
                result.append(maps[src][dest])

        return result
```

## Approach
- Standard graph problem
- Construct adjacency matrix from the given information 
- Since the weight of an edge connecting (a, b) is a/b, we can connect (b, a) by storing the weight as `1/(a/b)`. This allows to construct the complete two-way graph
- After that, we find the "distance" from one node to every other node and store these in a map. The algorithm for doing this is very similar to Dijkstra's, but does not use a minheap.
	- When finding the weight for a node adjacent to the one being currently examined, we multiply the weights instead of adding them.
	- This is because of the following. $\frac{a}{c} = \frac{a}{b} \cdot \frac{b}{c}$
	- This, combined with the reciprocation of weights allowing us to get a complete graph, makes the problem pretty straightforward
- Once we have the corresponding cost map for each node, we loop over the queries and check two things:
	- 1) The source node exists in the overall character map
	- 2) The destination node exists in the source node's cost map
- If either of these are not met, we append -1 to the result per the directions of the problem
- If both these conditions are true, we can simply append the cost (which represents `src/dest`)

**Category**: Graphs, Dijkstra's Algorithm


## Time and Space Complexity
- Time: $O(n^2)$
- Space: $O(n^2)$
## Similar Problems
- [[Leetcode/Leetcode]]