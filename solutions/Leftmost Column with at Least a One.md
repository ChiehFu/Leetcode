---
title: Leftmost Column with at Least a One
tags: Array, Easy
notebook: Leetcode
---

(This problem is an interactive problem.)

A binary matrix means that all elements are `0` or `1`. For each individual row of the matrix, this row is sorted in non-decreasing order.

Given a row-sorted binary matrix binaryMatrix, return leftmost column index(0-indexed) with at least a `1` in it. If such index doesn't exist, return `-1`.

You can't access the Binary Matrix directly.  You may only access the matrix using a BinaryMatrix interface:

- `BinaryMatrix.get(x, y)` returns the element of the matrix at index `(x, y)` (0-indexed).
- `BinaryMatrix.dimensions()` returns a list of 2 elements `[n, m]`, which means the matrix is `n * m`.
Submissions making more than `1000` calls to `BinaryMatrix.get` will be judged Wrong Answer.  Also, any solutions that attempt to circumvent the judge will result in disqualification.

For custom testing purposes you're given the binary matrix `mat` as input in the following four examples. You will not have access the binary matrix directly.

Example 1:

![alt](https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-5.jpg)
```
Input: mat = [[0,0],[1,1]]
Output: 0
```

Example 2:

![alt](https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-3.jpg)
```
Input: mat = [[0,0],[0,0]]
Output: -1
```

Example 3:

![alt](https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-6.jpg)
```
Input: mat = [[0,0,0,1],[0,0,1,1],[0,1,1,1]]
Output: 1
```

Constraints:

- 1 <= mat.length, mat[i].length <= 100
- mat[i][j] is either 0 or 1.
- mat[i] is sorted in a non-decreasing way.

----------
Thoughts:
1. For a sorted binary matrix of size (M, N), scan from `0` row `N - 1` col.
2. Once find a `0` in each row, proceed to the next row and start scanning from the position left to the leftmost index of value `1` we've found previously.
3. Keep track of the leftmost index of value `1` as scanning through the matrix.

```Java
// Time : O(M + N)
// Space: O(1)

/**
 * // This is the BinaryMatrix's API interface.
 * // You should not implement it, or speculate about its implementation
 * interface BinaryMatrix {
 *     public int get(int x, int y) {}
 *     public List<Integer> dimensions {}
 * };
 */

class Solution {
    public int leftMostColumnWithOne(BinaryMatrix binaryMatrix) {
    	List<Integer> dimension = binaryMatrix.dimensions();
    	int index = dimension.get(1);
    	
    	for (int i = 0; i < dimension.get(0); ++i) {
    		for (int j = index - 1; j >= 0; --j) {
    			if (binaryMatrix.get(i, j) == 0) {
    				break;
    			}
    			index = j;
    		}
    	}
    	
        return index == dimension.get(1)? -1 : index;
    }
}
```
