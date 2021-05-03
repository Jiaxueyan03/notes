```java
public class Test {

    public static void main(String[] args) {
        System.out.println(Arrays.toString(towSearch(new int[]{1,2,3,4,5,6,7},10)));
        System.out.println(Arrays.toString(towPoint(new int[]{1,2,3,4,5,6,7},10)));
    }

    public static int[] towSearch(int[] nums, int target){
        for(int i = 0; i < nums.length;i++){
            int low = i ,high = nums.length -1 ;
            int mid = low + (low + high)/2;
            if(nums[mid] == target - nums[i]){
                return new int[]{i,mid};
            }
            if(nums[mid] > target - nums[i]){
                high = mid -1;
            }
            if(nums[mid] < target - nums[i]){
                low = mid +1;
            }
        }
        return new int[0];
    }

    /**
     * 两数之和
     * 给定一个有序升序整数数组nums，从数组中找出两个数满足相加之和等于目标target
     * 假设每个输入只对应唯一的答案，而且不能使用相同的元素。
     * 返回两数的下标，以数组形式返回
     */
    public static int[] towPoint(int[] nums,int target){
        int low = 0,high = nums.length -1;
        while (low < high){
            int sum = nums[low] + nums[high];
            if(sum == target){
                return new int[]{low,high};
            }
            if(sum < target){
                low ++;
            }
            if(sum > target){
                high --;
            }
        }
        return new int[0];
    }
}
```