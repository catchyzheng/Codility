[760. Find Anagram Mappings](https://leetcode.com/problems/find-anagram-mappings/description/)<br>
题意：给定A B两个数组，是同样一串数字的不同排列。依次找出A中元素在B中的出现位置。<br>
解法：两个HashMap记录A B中各个数字位置，即mapA.put(A[i], i); mapB.put(B[i], i);之后依次返回mapB.get(A[i])即可。<br>
备注：鄙人用java在leetcode上做的第一道题。。语法上很不熟悉，折腾了很久才懂怎么用hashmap，然后hashmap中的元素get出来后要int强制转换才能用：(int)mapB.get(A[i])<br>
```
class Solution {
    public int[] anagramMappings(int[] A, int[] B) {
        int len = A.length;
        int[] ans = new int[len];
        HashMap mapA = new HashMap();
        HashMap mapB = new HashMap();
        for (int i=0;i<len;i++){
            mapA.put(A[i], i);
            mapB.put(B[i], i);
        }
        for(int i=0;i<len;i++){
            ans[i]=(int)mapB.get(A[i]);
        }
        return ans;
    }
}
```
[763. Partition Labels](https://leetcode.com/problems/partition-labels/description/)<br>
题意：给一串字母，尝试着划分尽可能多的子串，使得每个字母仅在一个子串中出现。<br>
解法：太久没有做题了。。想了好久才想出来。统计每个字母的首尾下标lef和rig。然后新建一个长度等于字符串长度的空数组t，遍历26个字母，在t中首尾下标区间内，[lef, rig)的元素都自增1。**为了便于统计，所以不记录rig元素。**然后t中每个非零子串长度即为答案。<br>
比如，1，3，2，0，4，2，0， 应当返回[4,3]。
```
class Solution {
    public List<Integer> partitionLabels(String s){
        int len = s.length();
        int[] min_ = new int[26];
        int[] max_ = new int[26];
        for(int i=0;i<26;i++){
        	min_[i]=max_[i]=0;
        }
        for(int i=0;i<len;i++){
            max_[s.charAt(i)-'a']=i;
        }
        for(int i=len-1;i>=0;i--){
            min_[s.charAt(i)-'a']=i;
        }
        int[] al= new int[len];
        for(int i=0;i<len;i++){
            al[i]=0;
        }
        for(int i=0;i<26;i++){
        	for(int j=min_[i]; j<max_[i];j++){
        		al[j]++;
        	}
        }
        List<Integer> l = new ArrayList();
        int cnt= 0;
        for(int i=0;i<len;i++){
            cnt++;
            if(al[i]==0){
                l.add(cnt); cnt=0;
            }
        }
        return l;
    }
}
```
[762. Prime Number of Set Bits in Binary Representation](https://leetcode.com/problems/prime-number-of-set-bits-in-binary-representation/description/)<br>
题意：给定两整数L,R，找出[L，R]内满足以下条件的数的个数：二进制表示有质数个1。L <= R in the range [1, 10^6]<br>
解法：最佳答案更简单。感觉代码能力被碾压。。<br>
For each number from L to R, let's find out how many set bits it has. If that number is 2, 3, 5, 7, 11, 13, 17, or 19, then we add one to our count. We only need primes up to 19 because R < 10^6 < 2^20 <br>
```
class Solution {
    public int countPrimeSetBits(int L, int R) {
        int ans = 0;
        for (int x = L; x <= R; ++x)
            if (isSmallPrime(Integer.bitCount(x)))
                ans++;
        return ans;
    }
    public boolean isSmallPrime(int x) {
        return (x == 2 || x == 3 || x == 5 || x == 7 ||
                x == 11 || x == 13 || x == 17 || x == 19);
    }
}
```
[754. Reach a Number](https://leetcode.com/problems/reach-a-number/description/)<br>
题意：从1开始，找到一个最短的序列，使得在前面添加正负号后，能够达到指定值。<br>
解法：从1开始累加，找到数N，使得加上N+1后和大于目标值**且差值能被2整除。**<br>
```
class Solution {
    public int reachNumber(int target) {
    	if(target<0) target = -target;
    	if(target==0) return 0;
    	if(target==2) return 3;
        int sum=0;
		int ans = -1;
        for(int i=1;;i++){
        	sum+=i;
        	if(sum==target){
        		ans=i; break;
        	}
        	else if(sum>target && (sum-target)%2==0){
        		ans = i;
                break;
        	}
        }
        return ans;
    }
}
```
[748. Shortest Completing Word](https://leetcode.com/problems/shortest-completing-word/description/)
题意：在words中找到一个最短的单词，其字母都来源于给定字符串。
解法：先去掉给定字符串中的非字母，然后words中的单词依次判断，记录最短长度。思路不难然而代码略长。
```
class Solution {
    public String shortestCompletingWord(String S, String[] words) {
        //Comparator cmp = new MyComparator();
        //Arrays.sort(words, cmp);
        Vector v = new Vector(7);
        for(int i=0;i<S.length();i++){
            if(Character.isWhitespace(S.charAt(i))) continue;
            if(Character.isDigit(S.charAt(i))) continue;
            if(Character.isUpperCase(S.charAt(i))){
                v.add(Character.toLowerCase(S.charAt(i)));
            }
            else v.add(S.charAt(i));
        }
        //System.out.println(v);
        String ans="";
        int len = 20;
        for(int i=0;i<words.length;i++){
            if(Can(words[i], v)){
                if(words[i].length()<len){
                	len = words[i].length();
                	ans = words[i];
                }
            }
        }
        return ans;
    }

    boolean Can(String word, Vector v){
        int cnt=0;
        for(int i=0;i<word.length();i++){
            if(Character.isUpperCase(word.charAt(i))){
                Character.toLowerCase(word.charAt(i));
            }
        }
        
        boolean[] used = new boolean[1000];
        for(int j=0;j<word.length();j++){
            used[j]=false;
        }
        for(int i=0;i<v.size();i++){
            for(int j=0;j<word.length();j++){
                if(!used[j] && word.charAt(j) == (Character)v.get(i)){
                    used[j]=true;
                    cnt++;break;
                }
            }
        }
        if(cnt==v.size()) return true;
        else return false;
    }
}
```

