## 剑指offer第八天
###  [剑指 Offer 16]数值的整数次方 Medium	
我的思路；递归奇偶数，但是有问题，数据量太大溢出
就是如果当n=Integer.MIN_VALUE的时候，第7行代码就会出问题，这是因为数字溢出问题，导致Integer.MIN_VALUE的相反数还是他自己，所以会一直调用，直到最后出现堆栈溢出异常。所以有一种方式就是把1/x提取出来一个，代码如下

public double myPow(double x, int n) {
    if (n == 0)
        return 1;
    //如果n小于0，把它改为正数，并且把1/x提取出来一个
    if (n < 0)
        return 1 / x * myPow(1 / x, -n - 1);
    return (n % 2 == 0) ? myPow(x * x, n / 2) : x * myPow(x * x, n / 2);
}


解题思路：位运算
 1.只有在1的位置上，才有相应的权重，这也就是为什么需要通过与运算：(b & 1) == 1判断最后一位是否为1。
2.a * 2 == a << 1，正负通用，即左移一位，二进制全体位数左移一位，整数翻倍，与普通运算一样有可能超出整型边界。
a / 2 == a >> 1，即带符号右移一位，二进制全体位数右移一位，最高位补原有符号位，
3.负数取倒数


class Solution {
    public double myPow(double x, int n) {
      if (x==0)
          return  0;
      long b =n ;
      double res =1.0;
      if (b <0){
          x=1/x ;
          b=-b;
      }
while(b>0){
    if((b&1)==1){
        res *=x;
    }
    x *=x;
    b>>=1;
}
return  res;
    }
}

### ✔ 	[剑指 Offer 17]打印从1到最大的n位数	77.7%	Easy	0.0%

我的思路：遍历
class Solution {
    public int[] printNumbers(int n) {
        int end =(int)Math.pow(10,n)-1;
        int[] res=new int[end];
        for (int i=0;i <end;i++)
            res[i]=i+1;
        return res;
    }
}