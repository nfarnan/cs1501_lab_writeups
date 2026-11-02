# Lab 2: Merge 2 Binary Trees (LeetCode 617) | Jack Carfrey
## Code
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        if (root1 == null) return root2;
        if (root2 == null) return root1;

        root2.val += root1.val;

        root2.left = mergeTrees(root1.left, root2.left);
        root2.right = mergeTrees(root1.right, root2.right);

        return root2;
    
    }
}
```
## Code Explanation
My code uses recursion to traverse through and merge the binary trees. I had a few different solutions that I came up with before I came to this one, but they all
used recursion to add to the root2 tree. This final solution is I think the most efficient and by far the shortest. It starts with the base cases.
The program checks if root1 is null, and if it is the program returns root2. It then checks if root2 is null, and if it is then it returns root1.
This makes the program much more efficient because instead of continuing through the subtrees of a node, it just returns the rest of the subtree.
Then, if neither node is null, then it adds the values of them together and puts it in root 2's node (since we're going to be returning this one).
Now, the program recurs through the left and right side. After all recursions are done, it will start returning root2, which is the node we want.
Once all recursions are done, it will return the head node of the now merged root2.
## Time and Space Complexity
I believe that the time complexity of this algorithm is O(n), where n is the amount of nodes in the tree with more nodes. This is because it has to go through and
either return the subtree or add the values of the nodes together for every node. It keeps making recursive nodes for each pair of nodes in the tree, but
once it hits a node that is null on root 1 or 2, it stops making recursive calls for the branch and returns just the other tree's collection of nodes,
which would be O(1) time (but not always, so overall is still O(n)).
For the space complexity, I think it is O(h), where h is the height of the taller tree. This is because all of the recursive calls srtack
on top of each other as the program iterates down the branches. However, since it only stacks up to a maximum of the height, the time
complexity is O(h) rather than O(n). If the tree is perfectly balanced, then h would be O(log n), but otherwise it would be O(n). In my
previous solutions, I had created new nodes which took up more space; however, this one does not create new nodes so no new space is used.
