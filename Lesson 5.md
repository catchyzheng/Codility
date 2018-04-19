(3)MinAvgTwoSlice<br>
题意：
还没做完。。日后再补
```
class Solution {
    public int solution(int[] A) {
        int len = A.length, end = len-1, sta=end-1;
        int min_index=sta, 
        double min_ = (A[end]+A[sta])/2.0;
        if(len==2) return min_;
        else{
            for(int i=sta;i>=0;i--){
            }
        }
    }
}
```

(2)PassingCars
题意：一个01数组,表示一辆车在该位置上要向左或者向右行驶。给定一辆车的位置，问一路上会遇到多少车。
解法：
```
class Solution {
    public int solution(int[] A) {
        int len = A.length;
        int[] cnt = new int[len];
        cnt[len-1]=A[len-1];
        for(int i=len-2;i>=0;i--){
            cnt[i]=A[i]+cnt[i+1];
        }
        int ans=0;
        for(int i=0;i<len;i++){
            if(A[i]==0){
                if(ans+cnt[i]>1000000000) {return -1;}
                else ans+=cnt[i];
            }
        }
        return ans;
    }
}
```

(1)CountDiv
题意：找出[a,b]中能被k整除的数的个数。
解法：要求时间空间复杂度均为O(1)。直接计算就行。
```
class Solution {
    public int solution(int a, int b, int k) {
        int first = (a/k)*k;
        if(first != a) first+=k;
        if(first>b) return 0;
        else{
            return (b-first)/k+1;
        }
    }
}
```
