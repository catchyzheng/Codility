(1) PermCheck<br>
题意：判断数组是不是一个排列。<br>
解法：设数组长度len，如果其中有元素大于len或者小于1，直接false。之后再用标记判断。<br>
```
class Solution {
    public int solution(int[] A) {
        int len = A.length;
        for(int i=0;i<len;i++){
            if(A[i]>len || A[i]<1) return 0;
        }
        boolean[] has = new boolean[len+1];
        for(int i=1;i<len+1;i++){
            has[i]=false;
        }
        for(int i=0;i<len;i++){
            has[A[i]]=true;
        }
        int yes = 1;
        for(int i=1;i<len+1;i++){
            if(has[i]==false){ yes = 0;break;}
        }
        return yes;
    }
}
```
(2)FrogRiverOne<br>
题意：寻找数组A中是否有1到X所有数。<br>
解法：直接判断。 <br>
```
class Solution {
    public int solution(int X, int[] A) {
        int sum = (1+X)*X/2;
        boolean[] have = new boolean[X+1];
        for(int i=1;i<=X;i++) have[i]=false;
        int ans = -1;
        for(int i=0;i<A.length;i++){
            if(!have[A[i]]){
                have[A[i]]=true;
                sum-=A[i];
                if(sum==0){ ans = i; break;}
            }
        }
        return ans;
    }
}
```
(3) MissingInteger<br>
题意：找到当前数组中未出现的最小的正整数。<br>
解法： 先找当前数组的最大值max_。如果最大值小于1，那么答案就是1。否则，新建一个长度max_+1的布尔数组，再扫描一遍A数组，从小到大找到第一个未出现的正整数，就是答案。<br>
```
class Solution {
    public int solution(int[] A) {
        int len = A.length;
        int max_=A[0];
        for(int i=1;i<len;i++){
            if(A[i]>max_) max_=A[i];
        }
        if(max_<=0) return 1;
        else{
            boolean[] has = new boolean[max_+1];
            for(int i=0;i<len;i++){
                if(A[i]>0) has[A[i]]=true;
            }
            int ans=max_+1;
            for(int i=1;i<=max_;i++){
                if(has[i]==false){ ans=i;break;}
            }
            return ans;
        }
    }
}
```
(4) MaxCounter<br>
题意：给定整数N和数组A，对于一个长度为N的数组ans，A[]代表了对它的一系列操作。按照以下规则操作数组ans：<br>
如果A[i]等于N+1，则ans全体设置为当前ans元素的最大值。否则，对ans中第A[i]个元素+1.<br>
求最后的ans。
解法：以下代码perform 77，效率不高。。日后看看如何改进 <br>
```
class Solution {
    public int[] solution(int N, int[] A) {
        int[] ans= new int[N];
        int max_=0;
        for(int i=0;i<A.length;i++){
            if(A[i]==N+1){
                for(int j=0;j<N;j++){
                    ans[j]=max_;
                }
            }
            else {
                ans[A[i]-1]++;
                if(max_<ans[A[i]-1]) max_=ans[A[i]-1];
            }
        }
        return ans;
    }
}
```