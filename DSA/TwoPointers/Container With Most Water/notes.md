##  Container With Most Water

- You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).
- Find two lines that together with the x-axis form a container, such that the container contains the most water.
- Return the maximum amount of water a container can store.
- Notice that you may not slant the container.
  

```
Example 1:

Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

Example 2:

Input: height = [1,1]
Output: 1
```
 
**Constraints**:

- n == height.length
- 2 <= n <= 105
- 0 <= height[i] <= 104

## Brute Force

- We are given vertical lines represented by an array of heights.
- The container is formed between any two lines.
- We need to find the pair of lines that together hold the maximum water.
- For every pair (i, j): Height of container = min(height[i], height[j]), Width of container = j - i and Area = height × width
- We will iterate through all pairs and get the max area.


```
class Solution {
    public int maxArea(int[] height) {
        int max=0;
        for(int i=0;i<height.length;i++){
            for(int j=i+1;j<height.length;j++){
                int h=Math.min(height[i],height[j]);
                int w=j-i;
                max=Math.max(max,h*w);
            }
        }
        return max;
    }
}
```

- **Time Complexity** - O(N*N)
- **Space Complexity** - O(1)

## Two Pointer

- Initialize two pointers: one at start and other at end .These represent the current two lines forming the container.
- Loop until l < r: Calculate the width between the lines: width = r - l, Calculate the height of the container: min(height[l], height[r])
and Calculate area and update max if it's greater.
- Move the pointer pointing to the shorter line:
- This is key for optimization. If the shorter line is on the left (height[l] <= height[r]), move l++.
- Else, move r--.
- Why? Because the height of the container is limited by the shorter line, and moving it might find a taller one, possibly increasing area.
- Repeat until the pointers meet.
- Return the maximum area found.

```
class Solution {
    public int maxArea(int[] height) {
        int max=0; 
        int l=0;
        int r=height.length-1;
        while(l<r){
            int width=r-l;
            max=Math.max(max,Math.min(height[l],height[r])*width);
            if(height[l]<=height[r]){
                l++;
            }
            else{
                r--;
            }
        }
        return max;
    }
}
```

- **Time Complexity** - O(N)
- **Space Complexity** - O(1)
