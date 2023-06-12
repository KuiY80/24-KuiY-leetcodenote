##     	[剑指 Offer 31]栈的压入、弹出序列	61.0%	Medium	0.0%
我的思路：引入一个栈push，pop 如果栈顶和目标不一样继续压榨，一样的的弹出 目标向下移位置
```
import java.util.ArrayDeque;
import java.util.Deque;

//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public boolean validateStackSequences(int[] pushed, int[] popped) {
        Deque<Integer> stack = new ArrayDeque<>();
        int n = pushed.length;
        for (int i = 0, j = 0; i < n; i++){
            stack.push(pushed[i]);
            while(!stack.isEmpty() && stack.peek()==popped[j]){
                stack.pop();
                j++;
            }
        }
        return stack.isEmpty();
    }
}
```


