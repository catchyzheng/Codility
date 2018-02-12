Lesson 1<br>
(1) BinaryGap<br>
题意：一个十进制数的二进制表示中，位于两个1之间的0的区间称为gap。找到这个数的最大gap。<br>
解法：思路不难，直接扫描二进制数组就行。但是，要注意，说的是两个1之间，也就并不是找最长0字符串。
score 100

Lesson 2<br>
(1) OddOccurrencesInArray<br>
题意：找到一个数组里只出现了一次的数字。**要求时间复杂度O(n)，空间复杂度O(1)。**<br>
解法：bingo！在诗兄帮助下知道了xor这个黑科技。。**所有元素xor后最后就是答案！**score 100<br>
```
class Solution {
    public int solution(int[] A) {
        int ans=A[0];
        if(A.length==1) return A[0];
        else{
            for(int i=1;i<A.length;i++){
                ans^=A[i];
            }
        }
        return ans;
    }
}
```

(2) CylicRotation<br>
题意：求指定数组循环右移后的结果。<br>
解法：模拟就行。注意数组判空。<br>
```
class Solution {
    public int[] solution(int[] A, int K) {
        if(A.length == 0 ) return new int[]{}; //zhuyi注意panduan注意判断kong注意判断空shuzu注意判断空数组。。
        int len = A.length;
        K = K % len;
        int[] ans = new int[len];
        for(int i=0;i<len;i++){
            ans[(i+K+len)%len]=A[i];
        }
        return ans;
    }
}
```
