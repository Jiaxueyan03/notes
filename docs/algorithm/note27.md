# 打家劫舍
## 首位不相连
```java
public class Rob {
    public static void main(String[] args) {
        int nums[] = new int[]{1,2,3,1};
        int nums1[] = new int[]{2,7,9,3,1};
        System.out.println(maxMoney(nums,nums.length-1));
        System.out.println(maxMoney(nums1,nums1.length-1));
        System.out.println(maxMoney1(nums));
        System.out.println(maxMoney1(nums1));
        System.out.println(maxMoney2(nums));
        System.out.println(maxMoney2(nums1));
    }

    /**
     * 打家劫舍
     * 你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有已定的现金，影响你偷窃的唯一制约因素
     * 就是相邻的房屋装有相互联通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。
     *
     * 给定一个代表每个房屋存放金额的非负整数数组，计算你不触动警报装置的情况下，一夜之内可以偷窃到的最高金额。
     *
     * 输入：[1,2,3,1] 输入：4
     * 输入：[2,7,9,3,1] 输入：12
     * @param nums
     * @param index
     * @return
     */
    static int maxMoney(int[] nums,int index){
       if(nums == null || index < 0){
           return 0;
       }
       if(index == 0){
           return nums[0];
       }
       return Math.max(maxMoney(nums,index-1),maxMoney(nums,index-2) + nums[index]);
    }

    // 最有子结构 n -> n-1 递归公司 重叠子变量
    static int maxMoney1(int[] nums){
        if(nums == null || nums.length == 0){
            return 0;
        }
        if(nums.length == 1){
            return nums[0];
        }
        int dp[] = new int[nums.length];
        dp[0] = nums[0];
        dp[1] = Math.max(nums[0],nums[1]);
        for (int i = 2;i<nums.length;i++){
            dp[i] = Math.max(dp[i-1],dp[i-2] + nums[i]);
        }
        return dp[nums.length-1];
    }

    static int maxMoney2(int[] nums){
        if(nums == null || nums.length == 0){
            return 0;
        }
        if(nums.length == 1){
            return nums[0];
        }
        int first = nums[0],seconed = nums[1];
        for (int i = 2;i<nums.length;i++){
          int temp = seconed;
          seconed = Math.max(first + nums[i],seconed);
          first = temp;
        }
        return seconed;
    }
}
```

## 首位相连
