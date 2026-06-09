# 624.[Maximum Distance in Arrays](https://leetcode.cn/problems/maximum-distance-in-arrays/description/)

question：

    You are given m arrays, where each array is sorted in ascending order.

    You can pick up two integers from two different arrays (each array picks one) and calculate the distance. We define the distance between two integers a and b to be their absolute difference |a - b|.

    Return the maximum distance.

py Solution：

    def maxDistance(self, arrays: List[List[int]]) -> int:
        preMin, preMax = arrays[0][0], arrays[0][len(arrays[0]) - 1]
        ans = -inf
        for i in range(1, len(arrays)):
            x, y = arrays[i][0], arrays[i][len(arrays[i]) - 1]
            ans = max(ans, max(preMax - x, y - preMin))
            preMax = max(preMax, y)
            preMin = min(preMin, x)
        return ans

cpp.Solution:

        class Solution { 
                public:
           int maxDistance(vector<vector<int>>& arrays) 
       {
    int dist=0;
    int max=arrays[0].back();
    int min=arrays[0].front();
    for(int i=1;i<arrays.size();i++)
    {
        dist=std::max(dist,std::max(arrays[i].back()-min,max-arrays[i].front()));
        max=std::max(arrays[i].back(),max);
        min=std::min(arrays[i].front(),min);
    }
    return dist;
       }
    };

# 美团第六场笔试第二题

question:

    有红蓝绿三种砖块，
    x块红砖可以合成1块蓝砖，
    
    y块蓝砖可以合成一块绿砖，但是不能反向合成。三种颜色的砖各一块称为“一套”，现在给出
    
    a块红砖，
    
    b块蓝砖，
    
    c块绿砖，同时给出了 x， y。请问出最多能得到砖的“套数”是多少。

py Solution:(二分查答案)

    a,b,c = map(int, input().split())
    x,y = map(int, input().split())

    left,right = 0, max(a,b,c)
    def check(s):
        if a<s: #红砖小于答案
            return  False
        p1 = a-s
        if b+p1//x< s: #蓝砖小于答案
            return False
        p2 = b+p1//x -s
        if c+p2//y <s:  #绿砖小于答案
            return False
        return True


    while left<=right:
        mid = (left+right)//2
        if check(mid):
            left = mid + 1 
        else:
            right = mid -1

    print(right)
