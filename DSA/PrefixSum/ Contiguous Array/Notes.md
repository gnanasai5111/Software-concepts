##  Contiguous Array

- Given a binary array nums, return the maximum length of a contiguous subarray with an equal number of 0 and 1.

```
Example 1:

Input: nums = [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with an equal number of 0 and 1.

Example 2:

Input: nums = [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.

Example 3:

Input: nums = [0,1,1,1,1,1,0,0,0]
Output: 6
Explanation: [1,1,1,0,0,0] is the longest contiguous subarray with equal number of 0 and 1.
```
 
**Constraints**:

- 1 <= nums.length <= 105
- nums[i] is either 0 or 1.

## Brute Force

- For every starting index i, check all subarrays beginning at i.
- Count the number of zeros and ones in the current subarray.
- Whenever the count of zeros equals the count of ones, update the maximum length.
- Repeat this for all subarrays.

```
class Solution {
    public int findMaxLength(int[] nums) {
        int max=0;
        for(int i=0;i<nums.length;i++){
            int ones=0;
            int zeros=0;
            for(int j=i;j<nums.length;j++){
                if(nums[j]==0){
                    zeros++;
                }
                else{
                    ones++;
                }
                if(zeros==ones){
                    max=Math.max(max,zeros+ones);
                }
            }
        }
        return max;
        
    }
}
```

- **Time Complexity** - O(N*N)
- **Space Complexity** - O(1)


## HashMap

- Convert the problem to a prefix sum problem by: Treating 1 as +1 and 0 as -1.
- If the sum becomes 0, it means the number of 0s and 1s are equal from the beginning till the current index → max = i + 1.
- If the same sum is seen again at a later index, the subarray between those indices has equal 0s and 1s.
- Why? Because the sum didn’t change, so the intermediate segment must have balanced out.
- Use a HashMap to store the first occurrence of each running sum.
- When the same sum reappears, calculate subarray length using: length = current_index - first_occurrence_index.
- Update max length accordingly.

```
class Solution {
    public int findMaxLength(int[] nums) {
        int sum=0,max=0;
        HashMap<Integer,Integer> map=new HashMap<>();
        for(int i=0;i<nums.length;i++){
           sum+= nums[i] == 1 ? 1 : -1;
           if(sum==0){
            max=i+1;
           }
           else if(map.containsKey(sum)){
            max=Math.max(max,i-map.get(sum));
           }
           else{
            map.put(sum,i);
           }
           
        }
        return max;
    }
}

```

- **Time Complexity** - O(N)
- **Space Complexity** - O(N)
