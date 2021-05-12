# String Search
```java
import java.util.Arrays;

public class KMP {

    public static void main(String[] args) {
        String str1 = "ABCABCAABCABCD";
        String str2 = "ABCABCD";
        int[] next = new int[]{str2.length()};
        getNext(str2.toCharArray(),next);
        int i = search(str1.toCharArray(),str2.toCharArray(),next);
        System.out.println(Arrays.toString(next));
        System.out.println(i);
        System.out.println(str1.indexOf(str2));
    }

    /**
     * String Search
     *
     * 给定两个字符串A、B，判断B在A中是否存在，存在返回A中的下标，不存在返回-1
     * 例：A：ABCABCAABCABCD
     *     B：ABCABCD
     * 返回值：7
     * @param str
     * @param pattern
     * @param next
     * @return
     */
    static int search(char[] str,char[] pattern,int[] next){
        int i = 0;
        int j = 0;
        while (i < str.length && j < pattern.length){
            if(j == -1 || str[i] == pattern[j]){
                i++;
                j++;
            }
            else {
                j = next[j];
            }
        }
        if(j == pattern.length){
            return i - j;
        }else {
            return -1;
        }
    }

    static void getNext(char[] pattern,int[] next){
        next[0] = -1;
        int i = 0,j=-1;
        while ( i < pattern.length){
            if(j == -1){
                i++;
                j++;
            }else if(pattern[i] == pattern[j]){
                i++;j++;
                next[i] = j;
            }eimport java.util.Arrays;

            public class KMP {

                public static void main(String[] args) {
                    String str1 = "ABCABCAABCABCD";
                    String str2 = "ABCABCD";
                    int[] next = new int[]{str2.length()};
                    getNext(str2.toCharArray(),next);
                    int i = search(str1.toCharArray(),str2.toCharArray(),next);
                    System.out.println(Arrays.toString(next));
                    System.out.println(i);
                    System.out.println(str1.indexOf(str2));
                }

                static int search(char[] str,char[] pattern,int[] next){
                    int i = 0;
                    int j = 0;
                    while (i < str.length && j < pattern.length){
                        if(j == -1 || str[i] == pattern[j]){
                            i++;
                            j++;
                        }
                        else {
                            j = next[j];
                        }
                    }
                    if(j == pattern.length){
                        return i - j;
                    }else {
                        return -1;
                    }
                }

                static void getNext(char[] pattern,int[] next){
                    next[0] = -1;
                    int i = 0,j=-1;
                    while ( i < pattern.length){
                        if(j == -1){
                            i++;
                            j++;
                        }else if(pattern[i] == pattern[j]){
                            i++;j++;
                            next[i] = j;
                        }else {
                            j = next[j];
                        }
                    }
                }
            }
            lse {
                j = next[j];
            }
        }
    }
}

```