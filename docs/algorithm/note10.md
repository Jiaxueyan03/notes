# 排列硬币-三种解法
```java
public class ArrangeCoin{

    public static void main(String[] args) {
        System.out.println(arrangeConis(10));
        System.out.println(arrangeConis2(10));
        System.out.println(arrangeCoins(10));
    }
    /**
     * 排列硬币
     * 总共有n枚硬币，将它们摆成一个阶梯形状，第k行就正好有k枚硬币，给定一个数字n，找出可形成完整阶梯行的总行数，
     * n是一个非负整数，并且在32位有符号整形范围。
     */

    // 暴力算法 迭代
    public static int arrangeConis(int n){
        for(int i= 1; i <= n;i ++){
            n = n-i;
            if(n <= i){
              return i;
            }
        }
        return 0;
    }

    // 二分查找
    public static int arrangeConis2(int n){
      int low= 0 ,high = n;
      while (low <= high){
          int mid = (low + high)/2 + low;
          int cost = (mid + 1) * mid/2;
          if(cost == mid){
              return mid;
          }
          if(cost > n){
              high = mid - 1;
          }else {
              low = mid + 1;
          }
      }
        return high;
    }

// 牛顿迭代 (x + n/x)/2
    public static int arrangeCoins(int n){
        if(n == 0){
            return 0;
        }
        return (int)sqrt(n,n);
    }

    private static double sqrt(double x,int n){
       double res = (x + (2 * n -x))/2;
       if(res == x){
           return x;
       }else {
           return sqrt(res,n);
       }
    }
}
```