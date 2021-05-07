# 省份数量
有n个城市，其中一些彼此相连，另一些没有相连。如果城市a与城市b直接相连，且城市b与城市c直接相连，那么城市a与城市c间接相连。
省份是一组直接或间接相连的城市，组内不含其他没有相连的城市。
给你一个n x n 的矩阵isConnectd，其中isConnectd[i][j] =1 表示第i个城市和第j个城市直接相连，而isConnectd[i][j] =0表示二者不直接相连。
返回矩阵中省份的数量。
扩展：朋友圈问题，亲戚问题。

```java
  public static void main(String[] args) {
        System.out.println(getProvince(new int[][]{{1,1,0},{1,1,0},{0,0,1}}));//2
        System.out.println(getProvince(new int[][]{{1,0,0},{0,1,0},{0,0,1}}));//3
    }

    // 深度优先 时间复杂度o(n*n) 空间复杂度 o(n)
    public static int getProvince(int[][] citysContected){
        int citys = citysContected.length;
        boolean[] visited = new boolean[citys];
        int provices = 0;// 计数器
        for (int i = 0 ; i< citys; i++){
            if(!visited[i]){
                // 深度优先
                dfs(i,citys,visited,citysContected);
                provices++;
            }
        }
        return  provices;
    }

    public static void dfs(int i,int citys,boolean[] visited,int[][] citysContected){
       for(int j =0;j <citys;j++){
           if(citysContected[i][j] == 1 && !visited[j] ){
               visited[j] = true;
               dfs(j,citys,visited,citysContected);
           }
       }
    }
```


```java
// 广度优先
 public static int bfs(int[][] citysContected){
        int citys = citysContected.length;
        boolean[] visited = new boolean[citys];
        int provices = 0;// 计数器
        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0 ; i< citys; i++){
            if(!visited[i]) {
                // 广度优先
                queue.offer(i);
                while (!queue.isEmpty()) {
                    int k = queue.poll();
                    visited[k] = true;
                    for (int j = 0; j < citys; j++) {
                        if (citysContected[i][j] == 1 && !visited[j]) {
                          queue.offer[j];
                        }
                    }
                }
                provices++;
            }
        }
        return  provices;
    }
```

```java
 // 并查集
    private static int mergeFind(int[][] citysContected){
        int citys = citysContected.length;;
        int[] head = new int[citys];
        int[] level = new int[citys];
        for (int i = 0;i<citys;i++){
            head[i]=i;
            level[i]=1;
        }
        for (int i = 0;i<citys;i++){
            for (int j =i+1 ;j<citys;j++){
              if(citysContected[i][j] ==1){
                  merge(i,j,head,level);
              }
            }
        }
        int count = 0;
        for (int i = 0;i<citys;i++){
           if(head[i] == i){
               count++;
           }
        }
        return count;
    }

    static void merge(int x,int y,int[] head,int[] level){
        int i = find(x,head);
        int j = find(y,head);
        if(i == j){
            return;
        }
        if(level[i] <= level[j]){
            head[i] = j;
        }else {
            head[j] = i;
        }
        if(level[i] == level[j]){
            level[i]++;
            level[j]++;
        }
    }

    private static int find(int x,int[] head){
        if(head[x] == x){
            return x;
        }
       head[x] = find(head[x],head);
        return head[x];

    }
```