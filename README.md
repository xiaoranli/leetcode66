# 10、leetcode66. 加一
==
解法一：
--  
思路：
--
    1、末位无进位，则末位加一即可，因为末位无进位，前面也不可能产生进位，比如 45 => 46。2、末位有进位，在中间位置进位停止，则需要找到进位的典型标志，即为当前位 %10 后为 0，则前一位加 1，直到不为 0 为止，比如 499 => 500。3、末位有进位，并且一直进位到最前方导致结果多出一位，对于这种情况，需要在第 2 种情况遍历结束的基础上，进行单独处理，比如 999 => 1000  
代码： 
--
<pre>
/**
 * @author lihe
 * @date 2019/10/16 14:50
 * @descriptor  66. 加一
 */
public class PlusOne_66 {
    public static int[] plusOne1(int[] digits) {
        for (int i = digits.length-1; i>=0; i--) {
            digits[i]++;
            digits[i] %= 10;
            if(digits[i] != 0)
                return digits;
        }
        int[] digit = new int[digits.length+1];
        digit[0] = 1;
        return digit;
    }

    public static void main(String[] args) {
        int[] arr = {9};
        int[] ints = plusOne1(arr);
        System.out.println(Arrays.toString(ints));
    }
}
</pre>

解法二：
--  
代码： 
--
<pre>
/**
 * @author lihe
 * @date 2019/10/16 14:50
 * @descriptor  66. 加一
 */
public class PlusOne_66 {
    public static int[] plusOne(int[] digits) {
        int[] sum = new int[digits.length+1];
        int i = digits.length;
        int K = 1;
        int j = 0;
        while(--i >= 0 || K > 0) {
            if(i >= 0)
                K = digits[i] + K;
            sum[j++] = K % 10;
            K = K / 10;
        }
        for (int k = 0; k < sum.length/2; k++) {
            swap(sum,k,sum.length-k-1);
        }
        if(sum[0]==0)
           sum = Arrays.copyOfRange(sum, 1, sum.length);
        return sum;
    }
    private static void swap(int[] sum, int k, int i) {
        int temp = sum[k];
        sum[k] = sum[i];
        sum[i] = temp;
    }
    public static void main(String[] args) {
        int[] arr = {9};
        int[] ints = plusOne1(arr);
        System.out.println(Arrays.toString(ints));

    }
}
</pre>
