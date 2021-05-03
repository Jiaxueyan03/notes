# 删除重复数组重的重复项

```java
 // 删除重复数组重的重复项
// 一个有序的数组nums，原地删除重复的元素，使每个数组只出现一次，返回删除后数组的新长度。
// 不能使用额外的数组空间，必须在原地修改输入数组并使用O(1）额外空间的条件下完成
// 输入：【0，1，2，2，3，3，4】 输出：5
// 重点考察双指针算法
public static void main(String[] args) {
    System.out.println(removeDuplicates(new int[]{0,1,2,2,3,3,4}));
}

public static int removeDuplicates(int[] nums){
    if(nums.length == 0){
        return 0;
    }
    int i = 0;
    for(int j = 1;j < nums.length ;j++){
        if(nums[j] != nums[i]){
            i ++ ;
            nums[i] = nums[j];
        }
    }
  return i + 1;
}
```


