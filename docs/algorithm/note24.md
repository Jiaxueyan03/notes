# 预测玩家
## 方法一递归
```java
/**
 * 预测玩家
 * 给定一个表示分数饿非负整数数组。玩家1从任意一端拿取一个分数，随后玩家2继续从剩余数组任意一端拿取分数，然后玩家1拿，......
 * 每次每个玩家只能拿取一个分数，分数被拿取之后不再可取。直到没有剩余分数可取时游戏结束。最终获得分数最多的玩家获胜。
 * 给定一个表示分数的数组，预测玩家1是否会成为赢家。你可以假设每个玩家玩法都会使他分数最大化。
 * 扩展：石子游戏
 */
public class CanWin {

    public static void main(String[] args) {
//        {5,200,1,3,6}
        int[] arr = new int[]{5,100,2,3};
        int sum = 0;
        for(int i : arr){
            sum+= i;
        }
        int p1= maxScore(arr,0,arr.length-1);
        System.out.println(p1> sum-p1);
        System.out.println(maxScore1(arr,0,arr.length-1));
    }

// 递归函数作用：统计分数 出口  范围递减的等式
    static int maxScore(int[] arr,int l,int r){
        if(r == l){
            return arr[l];
        }
        int sLeft = 0,rRight=0;
        if(r-l==1){
           sLeft=arr[l];
           rRight=arr[r];
        }
        if(r-l >=2){
            // sLeft = arr[l] + Math.min(maxScore(arr,l+2,r),maxScore(arr,l+1,r-1));
            // rRight = arr[r] + Math.min(maxScore(arr,l+1,r-1),maxScore(arr,l,r-2));
             int num = maxScore(arr,l+1,r-1);
            sLeft = arr[l] + Math.min(maxScore(arr,l+2,r),num);
            rRight = arr[r] + Math.min(num,maxScore(arr,l,r-2));
        }
        return Math.max(sLeft,rRight);
    }
}

static int maxScore1(int[] arr,int l,int r){
        if(r == l){
            return arr[l];
        }
        int sLeft = arr[l] - maxScore1(arr, l+1, r);
        int rRight = arr[r] - maxScore1(arr,l,r-1);
        return Math.max(sLeft,rRight);
    }

```


## 方法二 动态规划
```java
   // 动态规划 maxScore1(arr, l+1, r)存储到 [l+1][j] [l][j-1] dp数组
    static boolean dp(int[] arr){
//        int length = arr.length;
//        int[][] dp = new int[length][length];
//        for(int i = 0; i< length;i++){
//            dp[i][i] = arr[i];
//        }
//        for(int i = length-2;i>=0;i--){
//            for(int j = i+1; j<length;j++){
//                dp[i][j] = Math.max(arr[i] - dp[i+1][j],dp[i][j-1]);
//            }
//        }
//        return dp[0][length-1]>=0;
        int length = arr.length;
        int[] dp = new int[length];
        for(int i = 0; i< length;i++){
            dp[i] = arr[i];
        }
        for(int i = length-2;i>=0;i--){
            for(int j = i+1; j<length;j++){
                dp[j] = Math.max(arr[i] - dp[j],dp[j-1]);
            }
        }
        return dp[length-1]>=0;
    }
```
