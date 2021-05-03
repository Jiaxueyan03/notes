```java
public class AvgArray {

    public static void main(String[] args) {
        System.out.println(findMaxAverage(new int[]{1,12,-5,-6,50,3},4));
    }

    /**
     * 子数组最大平均数
     * 给定一个整数数组，找出平均数最大且长度为K的下标连续子数组，并输出该最大平均数
     * 输入：{1,12,-5,-6,50,3} k=4
     * 输出12。75
     * 最大平均数（12-5-6+50）/4=12。75
     * @param nums
     * @param k
     * @return
     */
    public static double findMaxAverage(int[] nums,int k){
        int sum = 0;
        int n = nums.length;
        for(int i= 0;i< k;i++){
            sum += nums[i];
        }
        int max = sum;
        for(int i = k; i< n;i++){
            sum = sum - nums[i-k] + nums[i];
            max = Math.max(sum,max);
        }
        return 1.0 * max/4;
    }
}
```