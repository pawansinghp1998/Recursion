Q.1.(104).Given the root of a binary tree, return its maximum depth.
A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Input: root = [3,9,20,null,null,15,7]
Output: 3

Input: root = [1,null,2]
Output: 2

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
    public int maxDepth(TreeNode root) {
        int lh=0;int rh=0;int h=0;
        if(root==null)
            return 0;
       lh=maxDepth(root.left);                        //first going to left until null is found,then right and we accordingly assigh the height of particular node
         rh=  maxDepth(root.right);
           return Math.max(lh,rh)+1;                  // +1 is added because height of currenrt node =height of node below current node+1
        
         }
}
