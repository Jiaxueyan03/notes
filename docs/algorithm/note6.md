# 寻找数组的中心下标

```java
 /**
 * 寻找数组的中心下标
 */
public class ArrayCenterIndex {

    // 寻找数组的中心下标
    // 给定一个整数数组nums，请写出一个能够返回数组'中心下标'的方法
    // 中心下标是数组的一个下标，其左侧所有元素相加的和等于右侧所有元素相加的和。
    // 如果数组不存在中心下标，返回-1。如果数组有多个中心下标，应该返回最靠近左侧的那个。注意：中心下标可能出现在数组的两端。
    public static void main(String[] args) {
        System.out.println(pivotIndex(new int[]{1,7,3,6,5,6}));
    }

    public static int pivotIndex(int[] nums){
        int sum = Arrays.stream(nums).sum();
        int total = 0;
        for(int i=0;i<nums.length;i++){
            total += nums[i];
            if(total == sum){
                return i;
            }
            sum = sum - nums[i];
        }
        return -1;
    }
}
```
