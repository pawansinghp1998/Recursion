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


Q.2.(110).Given a binary tree, determine if it is height-balanced.
For this problem, a height-balanced binary tree is defined as:a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

Input: root = [3,9,20,null,null,15,7]
Output: true

Input: root = [1,2,2,3,3,null,null,4,4]
Output: false

Input: root = []
Output: true
 
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
                
    public boolean isBalanced(TreeNode root) {
       if(root==null)
           return true;
        if(Math.abs(height(root.left)-height(root.right))<=1)             //calculating difference between height of left and right node o
            return (isBalanced(root.left)&& isBalanced(root.right));      //Checking condition at each node from top to bottom
        else
            return false;
    }
      public int height(TreeNode temp)
      {
          
         int lh=0;int rh=0;
          if(temp==null)
              return 0;
          lh=height(temp.left);
              rh=height(temp.right);
         
          return (Math.max(lh,rh)+1);              //returning the height of particular node to the calling function
      }
        
}
