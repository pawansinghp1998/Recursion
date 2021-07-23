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

Q.3.(1780).Given an integer n, return true if it is possible to represent n as the sum of distinct powers of three. Otherwise, return false.

An integer y is a power of three if there exists an integer x such that y == 3x.

 Input: n = 12
Output: true
Explanation: 12 = 31 + 32

Input: n = 91
Output: true
Explanation: 91 = 30 + 32 + 34

Input: n = 21
Output: false

class Solution { 
    int index=15;boolean z=false;int x=0;
    
    public boolean checkPowersOfThree(int n) {
      
        if(n==0)
            z= true;
        if(n>0 && index>0)                                       //Condition to enter into for loop and recursion
        {
            int i=0;
       for(i=0;i<index ;i++)                                       //Finding the maximum index so that Math.pow(3,index-1)<n  and also index can not repeat
       {
           if(Math.pow(3,i)>n)
           {
               index=i;
               break;
               }
         }
            index=index-1;                                   //this is done so that in next call index must be one less than previous condition if ,if condition of for loop does                                                                  not become true , and index value remain same for next iteration also
        x=(int)Math.pow(3,(index));
        checkPowersOfThree(n-x);                             //calling function recursively by changing value of n
    } 
       return z;
    }
}

Q.4.Given an encoded string, return its decoded string.
The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is being repeated exactly k times. Note that k is guaranteed to be a positive integer.You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.
Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, k. For example, there won't be input like 3a or 2[4].

Input: s = "3[a]2[bc]"
Output: "aaabcbc"

Input: s = "3[a2[c]]"
Output: "accaccacc"

Input: s = "2[abc]3[cd]ef"
Output: "abcabccdcdcdef"

Input: s = "abc3[cd]xyz"
Output: "abccdcdcdxyz"


class Solution {
    int index=0;
   
 public String decodeString(String s)
 {
     String res=helper(s,1).toString();
      return res; 
    }
    public StringBuilder helper(String s,int num)
    {
        StringBuilder sb=new StringBuilder();
        int x=0;
        while(index<s.length())
        {
            char c=s.charAt(index);
            index++;
            if(Character.isDigit(c))
            {
             x=x*10+(c-'0');
            }
            if(c=='[')
            {
                sb=sb.append(helper(s,x));
                x=0;
            }
            if(c ==']')
            {
                StringBuilder sb1=new StringBuilder();
                for(int i=0;i<num;i++)
                {
                sb1.append(sb);
                }
                return sb1;
            }
            if(Character.isLowerCase(c))
            {
                sb=sb.append(c);
            }
        }
        return sb;
    }
}
