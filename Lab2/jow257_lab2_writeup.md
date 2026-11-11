# My Implementation
``` # Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def mergeTrees(self, root1: TreeNode | None, root2: TreeNode | None) -> TreeNode | None:
        if root1 and root2:
            root1.val = root1.val+root2.val
            root1.left = self.mergeTrees(root1.left, root2.left)
            root1.right = self.mergeTrees(root1.right, root2.right)
        elif root1:
            root1.left = self.mergeTrees(root1.left, None)
            root1.right = self.mergeTrees(root1.right, None)
        elif root2:
            root1 = root2
            root1.left = self.mergeTrees(root1.left, None)
            root1.right = self.mergeTrees(root1.right, None)
        return root1
```
# What the code does and why
We are trying to return a tree that is tree 1 and tree 2 merged together. In my implementation I treat tree 1 as the tree that will be the sum of tree1 and tree2
There are three cases in the code:
 1. When the root of both trees are not null:
    Merge the root nodes by adding tree1.val and tree2.val together, then recursively merge the subtree of both left and right nodes.
 2. When only the second tree's root is null:
    Merge the root nodes by keeping tree1.val the same, then recursively merge the subtree of just root1. As I am writing this I realize that we could just return root1, since it is the only tree left and also the merged tree.
 3. When only the first tree's root is null
    Merge the root nodes by setting 'root1 = root2', then recursively merge the subtree of root1, which is now equal to root 2. As I am writing I realize that it would work to just set root 1 equal to root 2, then return root1, for the same reason as before.
# Runtime and memory analysis
The solution is O(n) runtime, as well as O(n), where n is the number of nodes of the larger binary tree, since we perform a function call on every node, each adding a new frame to the stack, and each function call performs a constant amount of work (n * 1) = n.
