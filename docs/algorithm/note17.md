# 柠檬水找零-贪心算法

```java
public class lemonChange {

    public static void main(String[] args) {
        System.out.println(change(new int[]{5,5,10}));
    }

    /**
     * 柠檬水找零
     * 在柠檬水摊上，每一杯柠檬水的售价为5美元。顾客排队购买你的产品，一次购买一杯。
     * 每位顾客只够买一杯柠檬水，然后向你付5美元，10美元或是20美元。必须给每位顾客正确找零。
     * 注意：一开始你手头没有任何零钱。
     * 如果你能给每位顾客正确找零返回true，否则返回false
     * @param bills
     * @return
     */
    public static boolean change(int[] bills){
        int five = 0,ten=0;
        for(int bill : bills){
            if(bill == 5){
                five++;
            }else if(bill == 10){
                if(five == 0){
                    return false;
                }
                five--;
                ten ++;
            }else {
                if(five > 0 && ten > 0){
                    five--;
                    ten--;
                }else if(five > 3){
                    five -= 3;
                }else {
                    return false;
                }
            }

        }
      return true;
    }
}
```