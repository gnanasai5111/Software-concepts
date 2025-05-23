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
- 

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


## HashMap

- As you traverse the array, store each element and its index in a HashMap.
- At each step, calculate the complement: target - current_element.
- Check if this complement already exists in the map: If yes, you've found the pair → return their indices.If no, store the current element and its index in the map.
- This way, you can find the required pair in one pass.

```
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        HashMap<Integer,Integer> map=new HashMap<>();
        for(int i=0;i<numbers.length;i++){
            int val=target-numbers[i];
            if(map.containsKey(val)){
                return new int[]{map.get(val)+1,i+1};
            }
            map.put(numbers[i],i);
        }
        return new int[]{};
    }
}

```

- **Time Complexity** - O(N)
- **Space Complexity** - O(N)

## Two Pointer

- Since the array is sorted, we can use the two-pointer technique. One at the start and other at the end.
- Calculate the sum of the elements at the two pointers:
- If the sum is equal to the target, return their indices (1-based).
- If the sum is less than the target, move the left pointer to the right to increase the sum.
- If the sum is greater than the target, move the right pointer to the left to decrease the sum.

```
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int left=0,right=numbers.length-1;
        while(left<right){
            if(numbers[left]+numbers[right]==target){
                return new int[]{left+1,right+1};
            }
            else if(numbers[left]+numbers[right]<target){
                left++;
            }
            else{
                right--;
            }
        }
        return new int[]{};
    }
}
```

- **Time Complexity** - O(N)
- **Space Complexity** - O(1)
