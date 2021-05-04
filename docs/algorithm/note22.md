# 二叉树遍历-层序-递归
```java
import java.util.ArrayList;
import java.util.Arrays;

public class BinaryTree {

    public static void main(String[] args) {
        TreeNode node7 = new TreeNode(7, null, null);
        TreeNode node6 = new TreeNode(6, null, null);
        TreeNode node5 = new TreeNode(5, node6, node7);
        TreeNode node4 = new TreeNode(4, null, null);
        TreeNode node3 = new TreeNode(3, null, null);
        TreeNode node2 = new TreeNode(2, node4, node5);
        TreeNode node1 = new TreeNode(1, node2, node3);
//        preorder(node1);
//        centerOrder(node1);
//        afterOrder(node1);
        ArrayList list = new ArrayList();
        levelOrder(node1,1,list);
        System.out.println(Arrays.toString(list.toArray()));
    }

    /**
     *二叉树遍历
     * 前序遍历：根左右
     * 中序遍历：左根右
     * 后序遍历：左右根
     * 层序遍历：从上往下，从左往右
     * 递归遍历：使用递归方法遍历
     * 迭代遍历：使用迭代方法实现递归函数，与递归等价，morris遍历
     */

    // 层序
    public static void levelOrder(TreeNode root,int  i , ArrayList list){
        if(root == null){
            return;
        }
        int length =  list.size();
        if(length <= i){
            for(int j = 0;j<=i-length;j++){
                list.add(length+j,null);
            }
        }
        list.set(i,root.val);
        levelOrder(root.left,2*i,list);
        levelOrder(root.right,2*i+1,list);
    }

     // 层序 上上往下 从左往右
    public static void levelOrder2(TreeNode root){
            Queue<TreeNode> queue = new LinkedList<>();
            queue.add(root);
            while (!queue.isEmpty()){
                TreeNode node = queue.poll();
                if(node != null){
                    System.out.println(node.val);
                    queue.add(node.left);
                    queue.add(node.right);
                }
            }
    }

    static class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;
        int deep;

        public TreeNode(){

        }

        public TreeNode(int val){
            this.val = val;
        }

        TreeNode(int val, TreeNode left, TreeNode right) {
            this.val = val;
            this.left = left;
            this.right = right;
        }
    }
}

```