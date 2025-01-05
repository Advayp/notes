- **Problem Link**:  https://leetcode.com/problems/sum-root-to-leaf-numbers/


## My Solution
```python
class Solution(object):
    def sumNumbers(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        self.res = 0 

        def traverse(node, curr_path):
            if not node:
                return

            if not node.right and not node.left:
                self.res += int(curr_path + str(node.val))
                return

            traverse(node.left, curr_path + str(node.val))
            traverse(node.right, curr_path + str(node.val))

        traverse(root, "")

        return self.res

```

## Approach
- Traverse the whole tree, keeping track of the current digit along the current path
	- Done recursively, exploring the left and right nodes and adding the value of the current node to the current path
- When the path reaches a leaf node, add the sum to the overall sum and return

**Category**: Binary Trees


## Time and Space Complexity
- Time: O(n)
- Space: O(1)
## Similar Problems
- [[Leetcode]]