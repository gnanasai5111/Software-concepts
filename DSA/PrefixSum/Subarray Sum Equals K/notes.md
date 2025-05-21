##  Subarray Sum Equals K

- Given an array of integers nums and an integer k, return the total number of subarrays whose sum equals to k.
- A subarray is a contiguous non-empty sequence of elements within an array.

```
Example 1:

Input: nums = [1,1,1], k = 2
Output: 2
Example 2:

Input: nums = [1,2,3], k = 3
Output: 2
```
 
**Constraints**:

- 1 <= nums.length <= 2 * 104
- -1000 <= nums[i] <= 1000
- -107 <= k <= 107

## Brute Force

- For every index, start a subarray from there.
- Keep adding numbers one by one to find the sum.
- Whenever the sum equals k, increase the count.
- Repeat this for all starting indexes.

```
class Solution {
    public int subarraySum(int[] nums, int k) {
        int count=0;
        for(int i=0;i<nums.length;i++){
            int sum=0;
            for(int j=i;j<nums.length;j++){
                sum=sum+nums[j];
                if(sum==k){
                    count++;
                }
            }
        }
        return count;
        
    }
}
```

- **Time Complexity** - O(N*N)
- **Space Complexity** - O(1)


## HashMap

- We're trying to count how many subarrays sum up to k.
- We're trying to count how many subarrays sum up to k.
- At every index, we keep track of the running sum (sum).
- If sum - k has been seen before, it means there’s a subarray ending at the current index which sums to k.
- sum is the current prefix sum at index i. sum - k means we’re looking for a previous prefix sum that would leave a subarray of sum k between that point and now.
- So, if sum - k is found in the map, we add its frequency to our count — because it means there are multiple subarrays that could result in the same sum.
- We also store the current sum in the map and update its frequency for future lookups.
- We initialize the map with map.put(0, 1) to handle cases where the prefix sum itself equals k at the start.

```
class Solution {
    public int subarraySum(int[] nums, int k) {
        int sum=0,count=0;
        HashMap<Integer,Integer> map=new HashMap<>();
        map.put(0,1);
        for(int i=0;i<nums.length;i++){
            sum=sum+nums[i];
            if(map.containsKey(sum-k)){
                count += map.get(sum - k);
            }
            map.put(sum,map.getOrDefault(sum, 0) + 1);
        }
        return count;
        
    }
}

```

- **Time Complexity** - O(N)
- **Space Complexity** - O(N)
