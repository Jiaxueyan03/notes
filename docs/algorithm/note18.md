```java
public class Triangles {

    public static void main(String[] args) {
        System.out.println(largesPerimeter(new int[]{3,6,2,3}));
    }

    /**
     *  三角形最大周长
     *  给定一些由整数（代表长度）组成的数组arr，返回由其中三个长度组成的面积不为零的三角形的最大周长。
     * 如果不能形成任何面积不为零的三角形，返回0
     * @param nums
     * @return
     */
    public static int largesPerimeter(int[] nums){
        Arrays.sort(nums);
        for(int i = nums.length-1;i>=2;i--){
          if(nums[i-1]+nums[i-1]>nums[i]){
              return nums[i-1]+nums[i-2]+nums[i];
          }
        }
        return 0;
    }
}
```