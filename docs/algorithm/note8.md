方法一：暴力递归
```java
 public static void main(String[] args) {
        System.out.println(calculate(10));
    }

    /**
     * 斐波那契数列
     * 求取斐波那契而数列的第N位的值
     * 斐波那契数列：每一位的值等于他前两位数字之和。前两位固定0，1，2，3，5，8.。。。
     */
    public static int calculate(int num){
        if(0==num){
            return 0;
        }
        if(1 == num){
            return 1;
        }
        return calculate(num -1) + calculate(num -2);
    }
```

方法二：去重递归
```java
 public static int calculate1(int num){
        int[] arr = new int[num + 1];
        return recurse(arr,num);
    }

    public static int recurse(int[] arr,int num){
        if(0 == num){
            return 0;
        }
        if(1 == num){
            return 1;
        }
        if(arr[num] != 0){
            return arr[num];
        }
        arr[num] = recurse(arr,num-1) + recurse(arr,num -2);
        return arr[num];
    }
```

方法三：双指针迭代
```java
 public static int iterate(int num){
        if(0 == num){
            return 0;
        }
        if(1 == num){
            return 1;
        }
        int low = 0,high = 1;
        for(int i = 2; i <= num ;i ++){
            int sum = low + high;
            low = high;
            high =sum;
        }
        return high;
    }
```