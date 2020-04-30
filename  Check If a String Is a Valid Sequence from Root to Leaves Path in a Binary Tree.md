---
title:  Check If a String Is a Valid Sequence from Root to Leaves Path in a Binary Tree
tags: Tree, Easy, DFS
notebook: Leetcode
---

Given a binary tree where each path going from the root to any leaf form a valid sequence, check if a given string is a valid sequence in such binary tree. 

We get the given string from the concatenation of an array of integers arr and the concatenation of all values of the nodes along a path results in a sequence in the given binary tree.

 

Example 1:

<img src='https://assets.leetcode.com/uploads/2019/12/18/leetcode_testcase_1.png' height="200">

```
Input: root = [0,1,0,0,1,0,null,null,1,0,0], arr = [0,1,0,1]
Output: true
Explanation: 
The path 0 -> 1 -> 0 -> 1 is a valid sequence (green color in the figure). 
Other valid sequences are: 
0 -> 1 -> 1 -> 0 
0 -> 0 -> 0
```

Example 2:

<img src='https://assets.leetcode.com/uploads/2019/12/18/leetcode_testcase_2.png' height="200">

```
Input: root = [0,1,0,0,1,0,null,null,1,0,0], arr = [0,0,1]
Output: false 
Explanation: The path 0 -> 0 -> 1 does not exist, therefore it is not even a sequence.
```

Constraints:

- 1 <= arr.length <= 5000
- 0 <= arr[i] <= 9
- Each node's value is between [0 - 9].

----------

```Java
//Time: O(N)
//Space: O(N)

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
    public boolean isValidSequence(TreeNode root, int[] arr) {
        return isValidSequence(root, arr, 0);
    }
    
    private boolean isValidSequence(TreeNode root, int[] arr, int index) {
    	if (root == null || index == arr.length) {
    		return false;
    	}
    	
    	if (root.val != arr[index]) {
    		return false;
    	}
        
        if (index == arr.length - 1) {
            return root.left == null && root.right == null;
        } 
        
    	return isValidSequence(root.left, arr, index + 1) || 
    		   isValidSequence(root.right, arr, index + 1);
    }
}
```