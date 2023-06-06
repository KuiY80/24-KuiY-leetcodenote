#     	[剑指 Offer 26]树的子结构	46.4%	Medium	0.0%
我的思路：二叉树是盲区
题解：递归 遍历
```
class Solution {
    public boolean isSubStructure(TreeNode A, TreeNode B) {
        if (A == null || B == null)
            return false;
        //先从根节点判断B是不是A的子结构，如果不是在分别从左右两个子树判断，
        //只要有一个为true，就说明B是A的子结构
        return isSub(A, B) || isSubStructure(A.left, B) || isSubStructure(A.right, B);
    }

    boolean isSub(TreeNode A, TreeNode B) {
        //这里如果B为空，说明B已经访问完了，确定是A的子结构
        if (B == null)
            return true;
        //如果B不为空A为空，或者这两个节点值不同，说明B树不是
        //A的子结构，直接返回false
        if (A == null || A.val != B.val)
            return false;
        //当前节点比较完之后还要继续判断左右子节点
        return isSub(A.left, B.left) && isSub(A.right, B.right);
    }
}
```
#     	[剑指 Offer 27]二叉树的镜像	79.6%	Easy	0.0%

思路：dfs从上到下遍历
```
class Solution {
    public TreeNode invertTree(TreeNode root) {
    if (root == null) {
     return root; 
     } // 将当前节点的左右子树交换 
     TreeNode tmp = root.left; root.left = root.right; root.right = tmp;
      // 递归交换当前节点的 左子树 
      invertTree(root.left); // 递归交换当前节点的 右子树 
      invertTree(root.right);
       return root;
    }
}
```