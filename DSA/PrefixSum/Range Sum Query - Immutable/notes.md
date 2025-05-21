## Range Sum Query - Immutable

- Given an integer array nums, handle multiple queries of the following type:
- Calculate the sum of the elements of nums between indices left and right inclusive where left <= right.
  
Implement the NumArray class:

- NumArray(int[] nums) Initializes the object with the integer array nums.
- int sumRange(int left, int right) Returns the sum of the elements of nums between indices left and right inclusive (i.e. nums[left] + nums[left + 1] + ... + nums[right]).

```
Example 1:

Input
["NumArray", "sumRange", "sumRange", "sumRange"]
[[[-2, 0, 3, -5, 2, -1]], [0, 2], [2, 5], [0, 5]]
Output
[null, 1, -1, -3]

Explanation
NumArray numArray = new NumArray([-2, 0, 3, -5, 2, -1]);
numArray.sumRange(0, 2); // return (-2) + 0 + 3 = 1
numArray.sumRange(2, 5); // return 3 + (-5) + 2 + (-1) = -1
numArray.sumRange(0, 5); // return (-2) + 0 + 3 + (-5) + 2 + (-1) = -3
```
 
**Constraints**:

- 1 <= nums.length <= 104
- -105 <= nums[i] <= 105
- 0 <= left <= right < nums.length
- At most 104 calls will be made to sumRange.

## Brute Force

- Copy the given array into a global array.
- For each sumRange(left, right) call, traverse the range and calculate the sum manually.

```
class NumArray {
    int[] originalArray;
    public NumArray(int[] nums) {
        originalArray = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            originalArray[i] = nums[i];
        }
    }
    
    public int sumRange(int left, int right) {
        int totalSum = 0;
        for (int i = left; i <= right; i++) {
            totalSum += originalArray[i];
        }
        return totalSum;
    }
}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * int param_1 = obj.sumRange(left,right);
 */
```

**Time Complexity** - O(N) in constructor, and O(N) for each sumRange call
**Space Complexity** - O(N)


## Prefix sum

- When we build the preSum array, we do this: preSum[i] stores the sum of all elements from index 0 to i - 1.
- If we want to find the sum from index left to right, we don’t need to loop — we can subtract the sum before left from the sum before right + 1.

```
class NumArray {
    int[] preSum;
    public NumArray(int[] nums) {
        preSum = new int[nums.length+1];
        for (int i = 1; i < preSum.length; i++) {
            preSum[i] = preSum[i-1]+nums[i-1];
        }
    }
    
    public int sumRange(int left, int right) {
        return preSum[right+1]-preSum[left];
    }
}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * int param_1 = obj.sumRange(left,right);
 */

```

**Time Complexity** - O(N) in constructor, and O(1) for each sumRange call
**Space Complexity** - O(N)
