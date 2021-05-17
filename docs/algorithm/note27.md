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
```java
public class Rob {
    public static void main(String[] args) {
        int nums[] = new int[]{1, 2, 3, 1};
        int nums1[] = new int[]{2, 7, 9, 3, 1};
        TreeNode node5 = new TreeNode(1,null,null);
        TreeNode node4 = new TreeNode(3,null,null);
        TreeNode node3 = new TreeNode(3,null,node5);
        TreeNode node2 = new TreeNode(2,null,node4);
        TreeNode node1 = new TreeNode(3,node2,node3);
        int[] i = dfs(node1);
        System.out.println(Math.max(i[0],i[0]));

    }
    /**
     * 二叉树
     *
     * @param nums
     * @return
     */
    static int maxMoney4(int[] nums, int start, int end) {
        int first = nums[start], second = Math.max(nums[start], nums[start + 1]);
        for (int i = start + 2; i <= end; i++) {
            int temp = second;
            second = Math.max(first + nums[i], second);
            first = temp;
        }
        return second;
    }

    /**
     * 打家劫舍3
     * 在上次打劫完一条接到之后和一圈房屋之后，小偷又发现了一个新的可行窃得地区。这个地区只有一个入口
     * ，我们称之为“根”。除了“根”之外，每栋房子有且只有一个“父”房子与之相连。一番侦察之后，聪明得小偷意识到“这个地方得所哟匢得排列类似于一棵二叉树”。
     * 如果两个直接相连得房子在同一天晚上被打劫，房屋将自动报警。
     * 计算在不触动警报得情况下，小偷一晚能到盗取得最高金额。
     *
     * 深度优先搜索
     * @param node
     * @return
     */
    public static int[] dfs(TreeNode node){
        // int[]{select的最优解,notSelect的最优解}
        if(null == node){
            return new int[]{0,0};
        }
        int[] l = dfs(node.left);
        int[] r = dfs(node.right);
        int select = node.val + l[1]+r[1];
        int notSelect = Math.max(l[0],l[1]) + Math.max(r[0],r[1]);
        return new int[]{select,notSelect};
    }


    static class TreeNode{
        int val;
        TreeNode left;
        TreeNode right;
        int deep;
        TreeNode(int val){
            this.val=val;
        }
        TreeNode(int val,TreeNode left,TreeNode right){
            this.val=val;
            this.left=left;
            this.right=right;
        }
    }
}

```