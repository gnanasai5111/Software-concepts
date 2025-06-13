## Daily Temperatures

- Given an array of integers temperatures represents the daily temperatures, return an array answer such that answer[i] is the number of days you have to wait after the ith day to get a warmer temperature. If there is no future day for which this is possible, keep answer[i] == 0 instead.

```
Example 1:

Input: temperatures = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]

Example 2:

Input: temperatures = [30,40,50,60]
Output: [1,1,1,0]

Example 3:

Input: temperatures = [30,60,90]
Output: [1,1,0]
```

**Constraints**:
- 1 <= temperatures.length <= 105
- 30 <= temperatures[i] <= 100


## Brute Force

- For each day i, checks all future days j to find the first day with a higher temperature
- If a warmer day is found, stores the difference j - i in the result array
- If no warmer day exists in the future, the result remains 0 (default value)

```
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int res[]=new int[temperatures.length];
        for(int i=0;i<temperatures.length;i++){
            for(int j=i+1;j<temperatures.length;j++){
                if(temperatures[j]>temperatures[i]){
                    res[i]=j-i;
                    break;
                }
            }
        }
        return res;
        
    }
}
```

**Time complexity** - O(N*N)
**Space Complexity** - O(N)


## Monotonic stack 

- Solves the Daily Temperatures problem using a monotonic decreasing stack
- Iterates the temperatures array from right to left
- Maintains a stack of indices where temperatures are in decreasing order
- Pops indices from the stack while the current temperature is greater than or equal to the temperature at the stack's top index
- If the stack is empty, there is no warmer day ahead, so stores 0
- If the stack is not empty, stores the difference between the next warmer day's index and the current index
- Pushes the current index onto the stack after processing

```
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int res[]=new int[temperatures.length];
        Stack<Integer> st=new Stack<>();
        for(int i=temperatures.length-1;i>=0;i--){
            while(!st.isEmpty() && temperatures[i]>=temperatures[st.peek()]){
                st.pop();
            }
            res[i]=st.isEmpty()?0:st.peek()-i;
            st.push(i);
        }
        return res;
        
    }
}
```

**Time complexity** - O(N)
**Space Complexity** - O(N)
