##     	[剑指 Offer 33]二叉搜索树的后序遍历序列	56.9%	Medium	0.0%
题解思路：1.BST 的特点是左子树元素都小于根节点，右子树元素都大于根节点
2.后序遍历结果的特点是：左边一部分是左子树，右边一部分是右子树，最后一个元素是根节点。
```
class Solution {
    public boolean verifyPostorder(int[] postorder) {
        return check(postorder, 0, postorder.length - 1);
    }
    // 定义：检查 postorder[i..j] 是否是一个合法的 BST
    boolean check(int[] postorder, int i, int j) {
        if (i >= j) { return true;
        }
        // 根节点的值是后序遍历结果的最后一个元素
        int root = postorder[j];

    // postorder[i..left) 是左子树，应该都小于 root
        int left = i; while (left < j && postorder[left] < root) { left++; }
        // postorder[left..j) 是右子树，应该都大于 root
        int right = left;
        while (right < j && postorder[right] > root) {
            right++;
        }
        if (right != j) {
            return false;
        } // 递归检查左子树 [i..left) 和右子树 [left..j) 也符合 BST 的性质
         return check(postorder, i, left - 1) && check(postorder, left, j - 1); }
}
```
###    	[剑指 Offer 34]二叉树中和为某一值的路径	59.0%	Medium	0.0%
解题思路：
先序遍历： 按照 “根、左、右” 的顺序，遍历树的所有节点。
路径记录： 在先序遍历中，记录从根节点到当前节点的路径。当路径为 ① 根节点到叶节点形成的路径 且 ② 各节点值的和等于目标值 sum 时，将此路径加入结果列表。
算法流程：
pathSum(root, sum) 函数：
初始化： 结果列表 res ，路径列表 path 。
返回值： 返回 res 即可。

recur(root, tar) 函数：
递推参数： 当前节点 root ，当前目标值 tar 。
终止条件： 若节点 root 为空，则直接返回。
递推工作：
路径更新： 将当前节点值 root.val 加入路径 path ；
目标值更新： tar = tar - root.val（即目标值 tar 从 sum 减至 00 ）；
路径记录： 当 ① root 为叶节点 且 ② 路径和等于目标值 ，则将此路径 path 加入 res 。
先序遍历： 递归左 / 右子节点。
路径恢复： 向上回溯前，需要将当前节点从路径 path 中删除，即执行 path.pop() 。

值得注意的是，记录路径时若直接执行 res.append(path) ，则是将 path 对象加入了 res ；后续 path 改变时， res 中的 path 对象也会随之改变。

正确做法：res.append(list(path)) ，相当于复制了一个 path 并加入到 res 。

```
class Solution {
    LinkedList<List<Integer>> res = new LinkedList<>();
    LinkedList<Integer> path = new LinkedList<>(); 
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        recur(root, sum);
        return res;
    }
    void recur(TreeNode root, int tar) {
        if(root == null) return;
        path.add(root.val);
        tar -= root.val;
        if(tar == 0 && root.left == null && root.right == null)
            res.add(new LinkedList(path));
        recur(root.left, tar);
        recur(root.right, tar);
        path.removeLast();
    }
}

```


+


