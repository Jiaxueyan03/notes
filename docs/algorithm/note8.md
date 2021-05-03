# 两数之和-无序数组

```java
/**
 * 两数之和
 * 给定一个整数数组nums，从数组中找出两个数满足相加之和等于目标target
 * 假设每个输入只对应唯一的答案，而且不能使用相同的元素。
 * 返回两数的下标，以数组形式返回
 */
public class Test {

    public static void main(String[] args) {
        System.out.println(Arrays.toString(solution(new int[]{1,2,3,4,5,6,7},10)));
        System.out.println(Arrays.toString(solution(new int[]{1,2,3,4,5,6,7},10)));
    }

    public static int[] solution(int[] nums,int target){
        for (int i = 0; i< nums.length;i++){
            for (int j=i + 1; j<nums.length;j++){
                if (nums[i] + nums[j] == target) {
                    return new int[]{i,j};
                }
            }
        }
        return new int[0];
    }

    public static int[] solution1(int[] nums,int target){
        Map<Integer,Integer> map = new HashMap<>();
        for (int i= 0;i<nums.length;i++){
            if(map.containsKey(target - nums[i])){
                return new int[]{map.get(target - nums[i]),i};
            }
            map.put(nums[i],i);
        }
        return new int[0];
    }
}
```