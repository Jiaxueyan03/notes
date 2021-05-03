# 三个数的最大面积--线性扫描

```java
 public class MaxProduct {

    public static void main(String[] args) {
        System.out.println(sort(new int[]{1,2,3,4,5,6}));
        System.out.println(getMaxMin(new int[]{1,2,3,4,5,6}));
    }

    /**
     * 排序算法时间复杂度 NlogN)
     * @param nums
     * @return
     */
    public static int sort(int[] nums){
        Arrays.sort(nums);
        int n = nums.length;
        return Math.max(nums[0]*nums[1]*nums[n-1],nums[n-1]*nums[n-2]*nums[n-3]);
    }

// 三个数的最大乘积，整形数组nums，在数组中找出由三个数字组成的最大乘积，并输出这个乘积。
    //乘积不会越界，重点考察线性扫描
    public static int getMaxMin(int[] nums){
        int min1= Integer.MAX_VALUE,min2= Integer.MAX_VALUE;
        int max1 = Integer.MIN_VALUE,max2 = Integer.MIN_VALUE,max3 = Integer.MIN_VALUE;
        for ( int x : nums){
            if(x < min1){
                min2= min1;
                min1 = x;
            } else if(x < min2){
                min2 = x;
            }

            if(x > max1){
                max3= max2;
                max2= max1;
                max1 = x;
            }else if(x > max2){
                max3 =max2;
                max2 = x;
            }else if(x > max3){
                max3 = x;
            }
        }
       return Math.max(min1*min2*max1,max1*max2*max3);
    }
}
```
