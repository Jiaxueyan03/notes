# 井字游戏
```java
public class TicTacToe {
    public static void main(String[] args) {
        System.out.println(validBoard(new String[]{"XXX","OXO","O O"}));
    }

   /**
     * 并字游戏
     * 用字符串数组作为井自游戏的游戏板board，判断该游戏板有没有可能最终形成游戏板是一个3*3
     * 数组，由字符"","X"和"O"组成。字符""代表一个空位。两个玩家轮流将字符放入空位，一个
     * 玩家执行X棋，另一个玩家执行O棋"X"和"O"只允许放置在空位中，不允许对已放有字符的位置进行填充。
     * 当有3个相同（且非空）的字符填充任何行、列或对角线时，游戏结束，board板生成。
     * @param board
     * @return
     */
    public static boolean validBoard(String[] board){
        // X赢了 X-O=1
        // O赢了 O -X =1
        // 胜负未分 X=O X- O =1
        int xCount = 0,oCount = 0;
        for(String row : board){
            for(char c: row.toCharArray()){
                if(c == 'X'){
                    xCount++;
                }
                if(c == 'O'){
                    oCount++;
                }
            }
        }
        if(xCount != oCount && xCount -oCount !=1){
            return false;
        }
        if(win(board,"XXX") && xCount - oCount !=1){
            return false;
        }
        if(win(board,"OOO") && oCount - xCount !=1){
            return false;
        }
        return true;
    }

    static boolean win(String[] board,String flag){
          for(int i = 0; i< 3;i++){
              // 纵向3连
              if(flag.equals("" + board[0].charAt(i)+ board[1].charAt(i)+board[2].charAt(i))){
                  return true;
              }
              if(flag.equals("" + board[i])){
                  return true;
              }
              // \
              if(flag.equals("" + board[0].charAt(0)+ board[1].charAt(1)+board[2].charAt(2))){
                  return true;
              }
              // \
              if(flag.equals("" + board[0].charAt(2)+ board[1].charAt(1)+board[2].charAt(0))){
                  return true;
              }
          }
          return true;
    }
}

```