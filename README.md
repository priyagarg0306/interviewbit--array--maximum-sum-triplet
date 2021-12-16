# interviewbit--array--maximum-sum-triplet


**--------> Question:**

Given an array A containing N integers.

You need to find the maximum sum of triplet ( Ai + Aj + Ak ) such that 0 <= i < j < k < N and Ai < Aj < Ak.

If no such triplet exist return 0.



Problem Constraints
3 <= N <= 105.

1 <= A[i] <= 108.



Input Format
First argument is an integer array A.



Output Format
Return a single integer denoting the maximum sum of triplet as described in the question.



Example Input
Input 1:

 A = [2, 5, 3, 1, 4, 9]
Input 2:

 A = [1, 2, 3]


Example Output
Output 1:

 16
Output 2:

 6


Example Explanation
Explanation 1:

 All possible triplets are:-
    2 3 4 => sum = 9
    2 5 9 => sum = 16
    2 3 9 => sum = 14
    3 4 9 => sum = 16
    1 4 9 => sum = 14
  Maximum sum = 16
Explanation 2:

 All possible triplets are:-
    1 2 3 => sum = 6
 Maximum sum = 6
 
 
**-------> Code:**
 
**Right Code:(O(nlogn))**
 int Solution::solve(vector<int> &A) {

  int ans=0,n=A.size(),maxi=0;
    vector<int> v(n);

    for(int i=n-1;i>=0;i--){
        if(i==n-1){
            v[i]=A[i];
        }else{
            v[i]=max(A[i],v[i+1]);
        }
    }

    set<int> s;
    s.insert(A[0]);

    for(int i=1;i<n;i++){
        s.insert(A[i]);
        auto it=s.find(A[i]);

        if(it!=s.begin() && v[i]!=A[i]){
            ans=(*--it)+A[i]+v[i];
            maxi=max(maxi,ans);
        }
    }

    return maxi;
}
                          
**Wrong code:(O(n3))**
                          
int Solution::solve(vector<int> &A) {

    int sum=0,maxi=0,n=A.size();

    for(int i=0;i<n-2;i++){
        for(int j=i+1;j<n-1;j++){
            if(A[j]>A[i]){
                for(int k=j+1;k<n;k++){
                    if(A[k]>A[j]){
                        sum=A[i]+A[j]+A[k];
                        maxi=max(maxi,sum);
                    }
                }
            }
        }
    }

    return maxi;
}
