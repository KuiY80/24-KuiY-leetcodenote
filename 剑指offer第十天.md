#     	[剑指 Offer 20]表示数值的字符串	25.2%	Medium	0.0%
我首先想到的是判断否false而不是判断是true，毕竟有这么多条件满足才能判断true，但是只要有一个条件不满足就可以判断false，最后代码的效率也还可以，那么接下来进入正题吧：

首先定义了四个flag，对应四种字符
是否有数字：hasNum
是否有e：hasE
是否有正负符号：hasSign
是否有点：hasDot
其余还定义了字符串长度n以及字符串索引index
先处理一下开头的空格，index相应的后移
然后进入循环，遍历字符串
如果当前字符c是数字：将hasNum置为true，index往后移动一直到非数字或遍历到末尾位置；如果已遍历到末尾(index == n)，结束循环
如果当前字符c是'e'或'E'：如果e已经出现或者当前e之前没有出现过数字，返回fasle；否则令hasE = true，并且将其他3个flag全部置为false，因为要开始遍历e后面的新数字了
如果当前字符c是+或-：如果已经出现过+或-或者已经出现过数字或者已经出现过'.'，返回flase；否则令hasSign = true
如果当前字符c是'.'：如果已经出现过'.'或者已经出现过'e'或'E'，返回false；否则令hasDot = true
如果当前字符c是' '：结束循环，因为可能是末尾的空格了，但也有可能是字符串中间的空格，在循环外继续处理
如果当前字符c是除了上面5种情况以外的其他字符，直接返回false
处理空格，index相应的后移
如果当前索引index与字符串长度相等，说明遍历到了末尾，但是还要满足hasNum为true才可以最终返回true，因为如果字符串里全是符号没有数字的话是不行的，而且e后面没有数字也是不行的，但是没有符号是可以的，所以4个flag里只要判断一下hasNum就行；所以最后返回的是hasNum && index == n
如果字符串中间有空格，按以上思路是无法遍历到末尾的，index不会与n相等，返回的就是false

```
class Solution {
    public boolean isNumber(String s) {
        // 字符数组
        char[] charArray = s.toCharArray();
        // 字符串长度
        int n = charArray.length;

        // 当前下标
        int index = 0;

        // 标记
        boolean hasNum = false, hasE = false;
        boolean hasSign = false, hasDot = false;

        // 将下标移动到非空格字符上
        while (index < n && charArray[index] == ' ') {
            index++;
        }

        // 当前下标尚未到达字符串末尾
        while (index < n) {
            // 当前字符
            char c = charArray[index];

            if (c >= '0' && c <= '9') {
                // 当前字符是数字 0~9
                hasNum = true;
            } else if (c == 'e' || c == 'E') {
                // 当前字符是 e / E
                if (hasE || !hasNum) {
                    // e / E 已经出现过，或者数字没有出现过，则该字符串必定无法表示数值，返回 false
                    return false;
                }
                hasE = true;
                hasNum = false;
                hasSign = false;
                hasDot = false;
            } else if (c == '+' || c == '-') {
                // 当前字符是正负号
                if (hasSign || hasNum || hasDot) {
                    // 如果已经出现过符号、数字、小数点，则该字符串必定无法表示数值，返回 false
                    return false;
                }
                hasSign = true;
            } else if (c == '.') {
                // 如果是小数点
                if (hasDot || hasE) {
                    // 如果已经出现过小数点、e / E ，则该字符串必定无法表示数值，返回 false
                    return false;
                }
                hasDot = true;
            } else if (c == ' ') {
                // 如果是空格，跳出循环
                break;
            } else {
                // 非法字符
                return false;
            }

            // 继续判断下一个字符
            index++;
        }

        // 如果当前下标尚未到达字符串末尾，则剩下的字符应当全部为空格，否则该字符串必定无法表示数值，返回 false
        for (; index < n; index++) {
            if (charArray[index] != ' ') {
                return false;
            }
        }

        return hasNum;
    }
}
```
tr029211
#      	[剑指 Offer 21]调整数组顺序使奇数位于偶数前面	65.0%	Easy	0.0%
我的思路：一个数组的话，就先遍历奇数，后遍历偶数
class Solution {
    public int[] exchange(int[] nums) {
        int n= nums.length;
        int index =0;
        int [] res =new int[];
        for (int num:nums){
            if (num%2==1){
                res[index++] =num;
            }
        }
        for (int num:nums){
            if (num% 2==0){
                res[index++]=num;
            }
        }
return res;
    }
}
题解思路：双指针一次遍历
class Solution {
    public int[] exchange(int[] nums) {
        int n = nums.length;
        int[] res = new int[n];
        int left = 0, right = n - 1;
        for (int num : nums) {
            if (num % 2 == 1) {
                res[left++] = num;
            } else {
                res[right--] = num;
            }
        }
        return res;
    }
}