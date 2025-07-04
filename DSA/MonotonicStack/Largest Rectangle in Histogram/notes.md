## Largest Rectangle in Histogram

- Given an array of integers heights representing the histogram's bar height where the width of each bar is 1, return the area of the largest rectangle in the histogram.

```
Example 1:

Input: heights = [2,1,5,6,2,3]
Output: 10
Explanation: The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.

Example 2:

Input: heights = [2,4]
Output: 4
```

**Constraints**:
- 1 <= heights.length <= 105
- 0 <= heights[i] <= 104


## Brute Force

- For each bar i, expands to the left and right as long as bars are greater than or equal to the current bar's height
- Calculates the width of the rectangle that can be formed with height heights[i]
- Computes area as width * heights[i] and updates the maximum area found so far



```
class Solution {
    public int largestRectangleArea(int[] heights) {
        int max=0;
        for(int i=0;i<heights.length;i++){
            int index=i;
            int width=1;
            for(int j=index-1;j>=0;j--){
                if(heights[j]<heights[i]){
                    break;
                }
                width++;
            }
            for(int j=index+1;j<heights.length;j++){
                if(heights[j]<heights[i]){
                    break;
                }
                width++;
            }
            max=Math.max(max,width*heights[i]);
        }
        return max;
        
    }
}
```

**Time complexity** - O(N*N)
**Space Complexity** - O(1)


## Monotonic stack 



**Time complexity** - O(N)
**Space Complexity** - O(N)
