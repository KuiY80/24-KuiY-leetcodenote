
##     	[剑指 Offer 32 - I]从上到下打印二叉树	63.2%	Medium	0.0%
题解思路：bfs遍历树
```
       class Solution {
    public int[] levelOrder(TreeNode root) {
        if (root ==null) return new int[0];
        //队列初始化时添加
        Queue<TreeNode> queue = new LinkedList<>(){{add(root);}};
        ArrayList<Integer> ans = new ArrayList<>();
        while(!queue.isEmpty()) {
            TreeNode node = queue.poll();
            ans.add(node.val);
            if(node.left != null) queue.add(node.left);
            if(node.right != null) queue.add(node.right);
        }
        int[] res = new int[ans.size()];
        for(int i = 0; i < ans.size(); i++)  res[i] = ans.get(i);
        return res;

    }
}
```
##    	[剑指 Offer 32 - II]从上到下打印二叉树 II	68.9%	Easy	0.0%
题解：
```
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
//保存最终结果
        List<List<Integer>> res = new ArrayList<>();
        //保存每层数据
        List<Integer> temp = new ArrayList<>();
        //队列
        Queue<TreeNode> q = new LinkedList<>();
        //加入队列
        q.add(root);
        //使用null作为分层符
        q.add(null);
        //如果队列不为空
        while(!q.isEmpty()){
            //弹出队头节点
            TreeNode n = q.poll();
            //如果是分层符，说明这个分层符已经是最后一个最后一个元素了
            //所以退出循环
            if(n==null){
                break;
            }
            //如果不是分层符而是结点则添加它的值
            temp.add(n.val);
            //如果该节点左子节点不为空，则将其进队列
            if(n.left!=null){
                q.add(n.left);
            }
            //如果该结点右子节点不为空，则将其进队列
            if(n.right!=null){
                q.add(n.right);
            }
            //如果队列不为空且队头元素为空，则说明这层遍历完毕了
            //（至于为什么要判断队列是否为空，是因为队列为空时q.peek()得到的值也为null）
            if(!q.isEmpty()&&q.peek()==null){
                //将该层数据添加到结果中
                res.add(temp);
                //重置保存新一轮数据的集合
                temp = new ArrayList<>();
                //将队头的poll弹出
                q.poll();
                //在队尾加上null分层符，此时null前面的元素就属于一层的了
                q.add(null);
            }
        }
        //返回结果
        return res;
    }
}
```

##    	[剑指 Offer 32 - III]从上到下打印二叉树 III	58.2%	Medium	0.0%
题解思路：此方法的优点是只用列表即可，无需其他数据结构。
偶数层倒序： 若 res 的长度为 奇数 ，说明当前是偶数层，则对 tmp 执行 倒序 操作。
```
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        List<List<Integer>> res = new ArrayList<>();
        if(root != null) queue.add(root);
        while(!queue.isEmpty()) {
            List<Integer> tmp = new ArrayList<>();
            for(int i = queue.size(); i > 0; i--) {
                TreeNode node = queue.poll();
                tmp.add(node.val);
                if(node.left != null) queue.add(node.left);
                if(node.right != null) queue.add(node.right);
            }
            if(res.size() % 2 == 1) Collections.reverse(tmp);
            res.add(tmp);
        }
        return res;
    }
}

```