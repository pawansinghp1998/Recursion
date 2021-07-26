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

Q.5.(486).You are given an integer array nums. Two players are playing a game with this array: player 1 and player 2.

Player 1 and player 2 take turns, with player 1 starting first. Both players start the game with a score of 0. At each turn, the player takes one of the numbers from either end of the array (i.e., nums[0] or nums[nums.length - 1]) which reduces the size of the array by 1. The player adds the chosen number to their score. The game ends when there are no more elements in the array.

Return true if Player 1 can win the game. If the scores of both players are equal, then player 1 is still the winner, and you should also return true. You may assume that both players are playing optimally.

Input: nums = [1,5,2]
Output: false
Explanation: Initially, player 1 can choose between 1 and 2. 
If he chooses 2 (or 1), then player 2 can choose from 1 (or 2) and 5. If player 2 chooses 5, then player 1 will be left with 1 (or 2). 
So, final score of player 1 is 1 + 2 = 3, and player 2 is 5. 
Hence, player 1 will never be the winner and you need to return false.

Input: nums = [1,5,233,7]
Output: true
Explanation: Player 1 first chooses 1. Then player 2 has to choose between 5 and 7. No matter which number player 2 choose, player 1 can choose 233.
Finally, player 1 has more score (234) than player 2 (12), so you need to return True representing player1 can win.



class Solution { 
    public int check(int nums[],int s, int e)
    {
        if(s==e)
        {
            return nums[e];
        }
        int a=nums[s]+Math.min(check(nums,s+2,e),check(nums,s+1,e-1));  //calculating max for player 1
        int b=nums[e]+Math.min(check(nums,s,e-2),check(nums,s+1,e-1));  //calculating max for player 1
        
        return Math.max(a,b);
    }
    public boolean PredictTheWinner(int[] nums) {
        if(nums.length %2==0)               //if no of element is even player 1 can choose either all odd or all even
        {
            return true;
        }
        int sum=0;
        for(int i=0;i<nums.length;i++)
        {
            sum=sum+nums[i];
        }
        return 2*check(nums,0,nums.length-1)>=sum;
    }
}

M2.class Solution { 
    public int check(int nums[],int s, int e)
    {
        if(s==e)
        {
            return nums[e];
        }
       // int a=nums[s]+Math.min(check(nums,s+2,e),check(nums,s+1,e-1));
       // int b=nums[e]+Math.min(check(nums,s,e-2),check(nums,s+1,e-1));
        
        int a=nums[s]-check(nums,s+1,e);
        int b=nums[e]-check(nums,s,e-1);
        return Math.max(a,b);
    }
    public boolean PredictTheWinner(int[] nums) {
        /*if(nums.length %2==0)
        {
            return true;
        }
        int sum=0;
        for(int i=0;i<nums.length;i++)
        {
            sum=sum+nums[i];
        }
        return 2*check(nums,0,nums.length-1)>=sum;*/
        return check(nums,0,nums.length-1)>=0;
    }
}

Q.6.(231).Given an integer n, return true if it is a power of two. Otherwise, return false.

An integer n is a power of two, if there exists an integer x such that n == 2x.

Example 1:

Input: n = 1
Output: true
Explanation: 20 = 1
Example 2:

Input: n = 16
Output: true
Explanation: 24 = 16
Example 3:

Input: n = 3
Output: false
Example 4:

Input: n = 4
Output: true
Example 5:

Input: n = 5
Output: false

class Solution {
    boolean z=false;
    public boolean isPowerOfTwo(int n) {
        if(n==1)
            z= true;
        else if(n%2!=0)
            z= false;
        else if(n<1)
            z= false;
        else
        {
                isPowerOfTwo(n/2);
            
        }
        return z;
    }
}
