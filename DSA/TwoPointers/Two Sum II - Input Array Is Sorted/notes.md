##  Two Sum II - Input Array Is Sorted

- Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 <= numbers.length.
- Return the indices of the two numbers, index1 and index2, added by one as an integer array [index1, index2] of length 2.
- The tests are generated such that there is exactly one solution. You may not use the same element twice.
- Your solution must use only constant extra space.

```
Example 1:

Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].
Example 2:

Input: numbers = [2,3,4], target = 6
Output: [1,3]
Explanation: The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3. We return [1, 3].
Example 3:

Input: numbers = [-1,0], target = -1
Output: [1,2]
Explanation: The sum of -1 and 0 is -1. Therefore index1 = 1, index2 = 2. We return [1, 2].
```
 
**Constraints**:

- 2 <= numbers.length <= 3 * 104
- -1000 <= numbers[i] <= 1000
- numbers is sorted in non-decreasing order.
- -1000 <= target <= 1000
- The tests are generated such that there is exactly one solution.

## Brute Force

- Iterate through each element in the array using index i.
- For every index i, iterate through all elements after it using index j (i.e., from i + 1 to end).
- Check if numbers[i] + numbers[j] == target.
- If the sum matches the target, return the 1-based indices [i + 1, j + 1].
- If no such pair is found after all iterations, return an empty array.

```
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        for(int i=0;i<numbers.length;i++){
            for(int j=i+1;j<numbers.length;j++){
                if(numbers[i]+numbers[j]==target){
                    return new int[]{i+1,j+1};
                }
            }
        }
        return new int[]{};
        
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
