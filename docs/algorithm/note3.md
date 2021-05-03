
方法一：暴力算法
```java
 public static void main(String[] args) {
        System.out.println(bf(100));
        System.out.println(eratosthenes(100));
    }


    public static int bf(int n) {
        int count = 0;
        for (int i = 2; i < n; i++) {
            count += isPrime(i) ? 1 : 0;
        }
        return count;
    }

    private static boolean isPrime(int x) {
       /* for (int i = 2 ; i< x ; i++){
            if(x % i == 0){
                return false;
            }
        }*/
        for (int i = 2; i * i <= x; i++) {
            if (x % i == 0) {
                return false;
            }
        }
        return true;
    }
```

方法二：埃筛法


```java
 public static int eratosthenes(int n) {
        int count = 0;
        boolean isPrime[] = new boolean[n];
        for (int i = 2; i < n; i++) {
            if (!isPrime[i]) {
                count++;
            /*    for (int j = 2 * i; j < n; j += i) {
                    isPrime[j] = true;
                }*/
            for(int j = i * i ; j < n ; j += i ){
                isPrime[j] = true;
               }
            }
        }
        return count;
    }

```
