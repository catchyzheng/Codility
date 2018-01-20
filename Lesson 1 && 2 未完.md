还没有score 100的题：Lesson 2<br>
(1) OddOccurrencesInArray


Lesson 1<br>
(1) BinaryGap<br>
题意：一个十进制数的二进制表示中，位于两个1之间的0的区间称为gap。找到这个数的最大gap。<br>
解法：思路不难，直接扫描二进制数组就行。但是，要注意，说的是两个1之间，也就并不是找最长0字符串。
score 100

Lesson 2<br>
(1) OddOccurrencesInArray<br>
题意：找到一个数组里只出现了一次的数字。<br>
解法：判断当前向量V中是否有该元素，如果没有就add，有就remove这个。最后剩下的就是答案。<br>
貌似有的复杂样例超时了。。 日后有空再看看怎么提升准确度。<br>
Correct 100 Perform 25 Score 66

```
class Solution {
    public int solution(int[] A) {
        int len = A.length;
        Vector V = new Vector(len);
        for(int i=0;i<len;i++){
            if(!V.contains(A[i])){
                V.add(A[i]);
            }
            else{
                V.removeElement(A[i]);
            }
        }
        int ans=0;
        for(int i=0;i<V.size();i++){
            ans = (Integer)V.get(i);
        }
        return ans;
    }
}
```
 改C++后，correct100 perform 75 score 88
```
int solution(vector<int> &A) {
    map<int, int> M;
    int size = A.size();
    for(int i=0;i<size;i++ ){
        M[A[i]]++;
    }
    int ans=0;
    for(map<int,int>::iterator it= M.begin(); it!=M.end();it++){
        //cout<<(*it).first<<endl;
        if((it->second)%2==1){ ans = it->first; break;}
    }
    return ans;
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
