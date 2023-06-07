#     	[剑指 Offer 28]对称的二叉树	57.6%	Easy	0.0%
解题思路：
```
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return root == null ? true : recur(root.left, root.right);
    }
    boolean recur(TreeNode L, TreeNode R) {
        if(L == null && R == null) return true;
        if(L == null || R == null || L.val != R.val) return false;
        return recur(L.left, R.right) && recur(L.right, R.left);
    }
}
```

#    	[剑指 Offer 29]顺时针打印矩阵	43.1%	Easy	0.0%
解题思路：确定好边界
```
class Solution {
    public int[] spiralOrder(int[][] matrix) {
        if(matrix.length == 0) return new int[0];
        int l=0,r= matrix[0].length-1,t=0,b = matrix.length - 1,x = 0;
        int[] res = new int[(r + 1) * (b + 1)];
        while(true) {
            //列在变，列为循环值
            for (int i = l; i <= r; i++) {
                res[x++] = matrix[t][i];
                // 从左到右
                } //从左往右的下一步是往下走，上边界内缩，故++t
         if(++t > b) break; //从上往下，行在变
             for (int i = t; i <= b; i++) {
                 res[x++] = matrix[i][r]; // 从上到下
                 } //从上往下的下一步是从右往左，右边界收缩，--r
            if(l > --r) break; //从右向左，列在变
             for (int i = r;i >= l; i--) {
             res[x++] = matrix[b][i]; // 从右到左
            } //从右往左的下一步是从下往上，下边界收缩，--b
            if(t > --b) break; //从下到上，行在变
             for (int i = b; i >= t; i--) {
             res[x++] = matrix[i][l]; // 从下到上
             } //从下到上的下一步是从左到右，左边界收缩，++l
            if(++l > r) break;
             }
             return res;


    }
}
```