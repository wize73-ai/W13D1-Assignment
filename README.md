# W13D1-Assignment


class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def dfs(self, root):
        if not root:
            return []

        stack, result = [root], []
        while stack:
            node = stack.pop()
            result.append(node.val)
            if node.right:
                stack.append(node.right)
            if node.left:
                stack.append(node.left)
        
        return result

    def binaryTreePaths(self, root):
        if not root:
            return []

        def construct_paths(node, path):
            if node:
                path += str(node.val)
                if not node.left and not node.right:  # if leaf node
                    paths.append(path)  # add path to paths list
                else:
                    path += '->'  # extend path
                    construct_paths(node.left, path)
                    construct_paths(node.right, path)

        paths = []
        construct_paths(root, "")
        return paths

# Example usage:
# Constructing the binary tree:
#       1
#      / \
#     2   3
#      \
#       5

root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(3)
root.left.right = TreeNode(5)

solution = Solution()
print(solution.dfs(root))  # [1, 2, 5, 3]
print(solution.binaryTreePaths(root))  # ["1->2->5", "1->3"]


root =
[1,2,3,null,5]

    1
   / \
  2   3
   \
    5


Visiting node: 1, Current path: 1
Visiting node: 2, Current path: 1->2
Visiting node: 5, Current path: 1->2->5
Leaf node found. Path: 1->2->5 added to paths
Visiting node: 3, Current path: 1->3
Leaf node found. Path: 1->3 added to paths
('All paths:', ['1->2->5', '1->3'])




this iterative code for DFS produced a result of 9ms and space of 11.78 Mb  very fast beats 94%, but space is poor beating only 20%

trying recursive:

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def dfs(self, root):
        result = []
        self._dfs_helper(root, result)
        return result

    def _dfs_helper(self, node, result):
        if node:
            result.append(node.val)
            self._dfs_helper(node.left, result)
            self._dfs_helper(node.right, result)

    def binaryTreePaths(self, root):
        if not root:
            return []

        def construct_paths(node, path):
            if node:
                path += str(node.val)
                if not node.left and not node.right:  # if leaf node
                    paths.append(path)  # add path to paths list
                else:
                    path += '->'  # extend path
                    construct_paths(node.left, path)
                    construct_paths(node.right, path)

        paths = []
        construct_paths(root, "")
        return paths

# Example usage:
# Constructing the binary tree:
#       1
#      / \
#     2   3
#      \
#       5

root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(3)
root.left.right = TreeNode(5)

solution = Solution()
print(solution.dfs(root))  # [1, 2, 5, 3]
print(solution.binaryTreePaths(root))  # ["1->2->5", "1->3"]


Recursive is much slower, running 22 ms in 11.85mb , beating 14%, 20%

Iterative is preferable in these situations, 13 ms difference is significant as recursive was 245% slower than iterative.


### For number of paths problem, given a DAG, provide the number of paths from root to target.

using a depth first search approach to mapping the nodes from the graph:

[[1, 2], [3], [3], []]

Start from node 0:
0
|
+---1
|   |
|   +---3
|
+---2
    |
    +---3

0 -> 1 -> 3
0 -> 2 -> 3

Starting DFS from node 0
Visiting node: 0, Current path: [0]
Exploring node: 1 from node: 0
Visiting node: 1, Current path: [0, 1]
Exploring node: 3 from node: 1
Visiting node: 3, Current path: [0, 1, 3]
Reached target node. Path: [0, 1, 3] added to result
Backtracking from node: 1
Exploring node: 2 from node: 0
Visiting node: 2, Current path: [0, 2]
Exploring node: 3 from node: 2
Visiting node: 3, Current path: [0, 2, 3]
Reached target node. Path: [0, 2, 3] added to result
Backtracking from node: 2
Backtracking from node: 0
('DFS complete. Result:', [[0, 1, 3], [0, 2, 3]])



class Solution:
    def allPathsSourceTarget(self, graph):
        def dfs(node, path):
            if node == len(graph) - 1:  # if we reached the target node
                result.append(path)
                return
            for next_node in graph[node]:
                dfs(next_node, path + [next_node])  # recursive call with updated path
        
        result = []
        dfs(0, [0])  # start DFS from node 0 with path [0]
        return result

#### Same as above in JavaScript

    