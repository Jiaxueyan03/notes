# 优势洗牌
```java
import java.util.Arrays;
import java.util.Deque;
import java.util.HashMap;
import java.util.LinkedList;
import java.util.Map;

public class HorseRacing {

    public static void main(String[] args) {
        int[] A = new int[]{10,24,8,32};//{8,10,24,32}
        int[] B = new int[]{13,25,25,11};//{11,13,25,25}
        System.out.println(Arrays.toString(advantageCount(A,B)));
    }

    /**
     * 优势洗牌 （贪心算法）
     * 给定两个大小相等的数组A和B，A相对于B的优势可以满足A[i] > B[i]的索引i是我数目来描述。
     *
     * 反馈A的任意排列，使其相对于B的优势最大化。
     * @param A
     * @param B
     * @return
     */
    public static int[] advantageCount(int[] A,int[] B){
        int[] sortB = B.clone();
        Arrays.sort(sortB);
        Arrays.sort(A);
        Map<Integer, Deque<Integer>> bMap = new HashMap<>();
        for(int b : B){
           bMap.put(b,new LinkedList<>()) ;
        }
        Deque<Integer> aq = new LinkedList<>();
        int j = 0;
        for(int a : A){
            if(a > sortB[j]){
                bMap.get(sortB[j++]).add(a);
            }else{
                aq.add(a);
            }
        }
        int[] ans = new int[A.length];
        for(int i = 0; i <B.length;i++){
          if(bMap.get(B[i]).size() > 0){
              ans[i] = bMap.get(B[i]).removeLast();
          }else {
              ans[i] = aq.removeLast();
          }
        }
        return ans;
    }
}

```