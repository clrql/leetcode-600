
  # kth-largest-sum-in-a-binary-tree

  ```python3
  # Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthLargestLevelSum(self, root: Optional[TreeNode], k: int) -> int:
        level_sum = defaultdict(int)
        queue = [(root, 0)]

        while queue:
            node, level = queue.pop(0)
            level_sum[level] += node.val
            if node.left:
                queue.append((node.left, level+1))
            if node.right:
                queue.append((node.right, level+1))

        if len(level_sum) < k:
            return -1

        largest_k = nlargest(k, level_sum.values())
        return largest_k[-1]

  ```
  