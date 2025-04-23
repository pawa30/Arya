import math

def minimax(d, i, is_max, scores, depth):
    if d == depth:
        return scores[i]
    fn = max if is_max else min
    return fn(minimax(d+1, i*2, not is_max, scores, depth),
              minimax(d+1, i*2+1, not is_max, scores, depth))

scores = [3, 5, 2, 9, 12, 5, 23, 23]
depth = int(math.log2(len(scores)))

print("The optimal value is:", minimax(0, 0, True, scores, depth))

C++ code :

#include<bits/stdc++.h>
using namespace std;
int minimax(int depth, int nodeIndex, bool isMax,
 int scores[], int h)
{
 if (depth == h)
 return scores[nodeIndex];
 if (isMax)
 return max(minimax(depth+1, nodeIndex*2, false, scores, h),
 minimax(depth+1,
nodeIndex*2 + 1, false, scores, h));
 return min(minimax(depth+1, nodeIndex*2, true, scores, h),

 minimax(depth+1,
nodeIndex*2 + 1, true, scores, h));
}
int log2(int n)
{
 return (n==1)? 0 : 1 + log2(n/2);
}
int main()
{
 int scores[] = {3, 5, 2, 9, 12, 5, 23, 23};
 int n = sizeof(scores)/sizeof(scores[0]);
 int h = log2(n);
 int res = minimax(0, 0, true, scores, h);
 cout
<< "The optimal value is : " << res <<
endl;
 return 0;
}
