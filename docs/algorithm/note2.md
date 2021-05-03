
# x的平凡根
在不使用sqrt(X)函数情况下，得到x平方根的整数部分。

方法一：二分查找
```java
 public class Sqrt {

    public static void main(String[] args) {
        System.out.println(binarySearch(24));
    }

    public static int binarySearch(int x){
        int index = -1,l=0,r=x;
        while (l <= r){
            int mid = l + (r-l)/2;
            if(mid * mid <= x){
                index =mid;
                l = mid +1;
            }else {
                r = mid - 1;
            }
        }
        return index;
    }
}
```

方法二：牛顿迭代


```java
  public static int newto(int x){
        if(x == 0){
            return 0;
        }
        return (int)sqri(x,x);
    }

    public static double sqri(double i,int x){
        double res = (i + x/i)/2;
        if(res == i){
            return i;
        }else {
            return sqri(res,x);
        }
    }

```
