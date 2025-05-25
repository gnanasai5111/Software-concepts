##  Maximum Average Subarray I

- You are given an integer array nums consisting of n elements, and an integer k.
- Find a contiguous subarray whose length is equal to k that has the maximum average value and return this value. Any answer with a calculation error less than 10-5 will be accepted.

```
Example 1:

Input: nums = [1,12,-5,-6,50,3], k = 4
Output: 12.75000
Explanation: Maximum average is (12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75
Example 2:

Input: nums = [5], k = 1
Output: 5.00000
```
 
**Constraints**:

- n == nums.length
- 1 <= k <= n <= 105
- -104 <= nums[i] <= 104

## Brute Force

- Initialize max as Integer.MIN_VALUE to keep track of the maximum average found so far.
- Iterate through each possible starting index i of subarrays of length k (from 0 to nums.length - k).
- For each index i, initialize sum = 0.
- Use a nested loop with index j from i to i + k - 1 to calculate the sum of the current subarray.
- After the inner loop, calculate the average: (double) sum / k.
- Update max using Math.max(max, average)

```
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        double max=Integer.MIN_VALUE;
        for(int i=0;i<=nums.length-k;i++){
            int sum=0;
            for(int j=i;j<i+k;j++){
                sum=sum+nums[j];              
            }
            max=Math.max(max,(double)sum/k);
        }
        return max;
    }
}
```

- **Time Complexity** - O(N*N)
- **Space Complexity** - O(1)


## Sliding Window

- Create a prefix sum array sum[] of the same size as nums[].
- Initialize sum[0] = nums[0].
- Fill the prefix sum array: For each i from 1 to nums.length - 1: sum[i] = nums[i] + sum[i - 1]
- The sum of the first k elements is sum[k - 1], so set res = sum[k - 1].
- For each i from k to nums.length - 1:
- Calculate sum of subarray ending at i using: sum[i] - sum[i - k]
- Update res with the maximum value.
- After the loop, return res / k to get the maximum average.

```
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int[] sum = new int[nums.length];
		sum[0] = nums[0];
        for(int i=1;i<nums.length;i++){
            sum[i]=nums[i]+sum[i-1];
        }
        double res=sum[k-1];
        for(int i=k;i<nums.length;i++){
            res=Math.max(res,sum[i]-sum[i-k]);
        }
        return res/k;
        
    }
}

```

- **Time Complexity** - O(N)
- **Space Complexity** - O(N)

## Sliding Window

- Start with a variable sum = 0 to store the sum of elements in the current window.
- First, add the first k elements (index 0 to k - 1) into sum. This creates the first window of size k.
- Store this initial window's sum into another variable res, which keeps track of the maximum sum seen so far.
- Now, slide the window one element at a time:
- For each new element from index k to end of array:
- Add the new element entering the window (nums[i]).
- Subtract the old element leaving the window (nums[i - k]).
- Update sum with this new window's total.
- Compare the new sum with res, and update res if the current sum is larger.
- After the loop finishes, return res / k to get the maximum average.

```
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        double sum=0;
        for(int i=0;i<k;i++){
            sum+=nums[i];
        }
        double res=sum;
        for(int i=k;i<nums.length;i++){
            sum+=nums[i]-nums[i-k];
            res=Math.max(res,sum);
        }
        return res/k;
        
    }
}

```

- **Time Complexity** - O(N)
- **Space Complexity** - O(1)
