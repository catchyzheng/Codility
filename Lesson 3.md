(1)FrogJmp <br>
题意：一个青蛙在x，每次可以跳d距离。要跳到y，问至少跳多少步。<br>
```
class Solution {
    public int solution(int x, int y, int d) {
        if((y-x)%d==0) return (y-x)/d;
        else return (y-x)/d+1;
    }
}
```

(2)PermMissingElem<br>
 题意：一个数组有N个数，每个出现一次，都在 [1..(N + 1)]内。找到没出现那个数。<br>
解法：自己最先想到先高斯求和得到sum，之后依次减掉数组的元素就行。结果correct100 perform才60。后来发现数组元素最大可以100000。int范围不够了吧。结果改成long之后，依然perform60。
```
    public int solution(int[] A) {
        int N = A.length;
        long sum = (1+N)*(2+N)/2;
        for(int i=0;i<N;i++){
            sum-=A[i];
        }
        return (int) sum;
    }
```
 后来改变思路，用标记的策略，就score100了。早知道就应该这样想的。只是三次循环而已。 <br>
```
    public int solution(int[] A) {
        int N = A.length;
        boolean[] has = new boolean[N+2];
        for(int i=1;i<=N+1;i++){
            has[i]=false;
        }
        has[0]=true;
        for(int i=0;i<N;i++){
            has[A[i]]=true;
        }
        int ans=-123;
        for(int i=1;i<=N+1;i++){
            //System.out.println(has[i]);
            if(has[i]==false){ ans=i; break;}
        }
        return ans;
    }
```

(3)  TapeEquilibrium<br>
题意：给一个数组，找到一个下标p，使得a[0],...a[p-1]之和与a[p]之后的和的绝对值差最小。<br>
先是很快打出下面这段代码， <br>
```
class Solution {
    public int solution(int[] A) {
        int sum = 0;
        int len = A.length;
        for(int i=0;i<len;i++){
            sum+=A[i];
        }
        int min_diff=sum;
        int left_sum=0, right_sum=sum;
        for(int i=0;i<len;i++){
            left_sum+=A[i]; right_sum-=A[i];
            if(Math.abs(left_sum-right_sum)<min_diff){
                min_diff = Math.abs(left_sum-right_sum);
            }
        }
        return min_diff;
    }
}
```
 后来发现，左右每个部分至少要有一个元素的。所以改成下面的版本。score 100 通过。<br>
```
class Solution {
    public int solution(int[] A) {
        int sum = 0;
        int len = A.length;
        for(int i=0;i<len;i++){
            sum+=A[i];
        }
        int left_sum=A[0], right_sum=sum-A[0];
        int min_diff= Math.abs(left_sum-right_sum);
        for(int i=2;i<len;i++){
            left_sum+=A[i-1]; right_sum-=A[i-1];
            if(Math.abs(left_sum-right_sum)<min_diff){
                min_diff = Math.abs(left_sum-right_sum);
            }
        }
        return min_diff;
    }
}
```