##  3Sum

- Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.
- Notice that the solution set must not contain duplicate triplets.
  

```
Example 1:

Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.

Example 2:

Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.

Example 3:

Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.
```
 
**Constraints**:

- 3 <= nums.length <= 3000
- -105 <= nums[i] <= 105

## Brute Force

- The goal is to find all unique triplets in the array nums such that their sum is zero.
- Uses a brute-force approach with three nested loops to check every combination of three elements.
- Iterates over all triplets (i, j, k) where i < j < k
- For each triplet, checks if nums[i] + nums[j] + nums[k] == 0.
- If true, calls sort() to get the sorted triplet and adds it to a HashSet for uniqueness.
- Using HashSet<List<Integer>>: Prevents duplicate triplets by storing sorted triplets.
- Converts the HashSet to a List before returning to maintain the expected output type.

```
class Solution {
    public List<Integer> sort(int a,int b,int c){
        int min = Math.min(a, Math.min(b, c));
        int max = Math.max(a, Math.max(b, c));
        int mid = a + b + c - min - max;
        return Arrays.asList(min,mid,max);
    }
    public List<List<Integer>> threeSum(int[] nums) {
        HashSet<List<Integer>> set=new HashSet<>();
        for(int i=0;i<nums.length;i++){
            for(int j=i+1;j<nums.length;j++){
                for(int k=j+1;k<nums.length;k++){
                    if(nums[i]+nums[j]+nums[k]==0){
                        List<Integer> list =sort(nums[i],nums[j],nums[k]);
                        set.add(list);
                    }
                }
            }
        }
        return new ArrayList<>(set);
        
    }
}
```

- **Time Complexity** - O(N*N*N)
- **Space Complexity** - O(N*N)


## HashMap

- We want to find all unique triplets in the array that sum to 0.
- A HashSet<List<Integer>> is used to store unique triplets and automatically avoid duplicates.
- Loop through each element i from index 0 to n-1, and for each i, use a HashMap<Integer, Integer> to find the third value.
- For each j = i+1 to n-1, calculate sum = nums[i] + nums[j].
- Check if -sum already exists in the map. If yes, we found a triplet: nums[i], nums[j], -sum.
- Use the helper sort(nums[i], nums[j], -sum) to return the triplet in sorted (ascending) order as a list:
- Add this sorted list into the set to ensure no duplicate triplets.
- After the loops, convert the HashSet to a List and return it.

```
class Solution {
    public List<Integer> sort(int a,int b,int c){
        int min = Math.min(a, Math.min(b, c));
        int max = Math.max(a, Math.max(b, c));
        int mid = a + b + c - min - max;
        return Arrays.asList(min,mid,max);
    }
    public List<List<Integer>> threeSum(int[] nums) {
        HashSet<List<Integer>> set=new HashSet<>();
        for(int i=0;i<nums.length;i++){
            HashMap<Integer,Integer> map=new HashMap<>();
            for(int j=i+1;j<nums.length;j++){
                int sum=nums[i]+nums[j];
                if(map.containsKey(-sum)){
                    set.add(sort(-sum,nums[i],nums[j]));
                }
                map.put(nums[j],j);
            }
        }
        return new ArrayList<>(set);
        
    }
}

```

- **Time Complexity** - O(N*N)
- **Space Complexity** - O(N*N)

## Two Pointer

- First, the array is sorted using Arrays.sort(nums) to help with: Skipping duplicates efficiently and Applying the two-pointer technique.
- A List<List<Integer>> res is used to store the resulting unique triplets.
- Loop through each index i from 0 to n - 1: If i > 0 and nums[i] == nums[i - 1], skip to avoid checking the same number again (prevents duplicate triplets).
- For each i, use two pointers: left = i + 1 (next element after i) and right = nums.length - 1 (last element).
- While left < right, calculate the sum: nums[i] + nums[left] + nums[right]:
- If the sum is 0, we found a valid triplet:
- Add it to the result list using Arrays.asList(...)
- Move left++ and right-- to look for the next possible pair
- Skip duplicates for left using while (left < right && nums[left] == nums[left - 1]) left++
- Skip duplicates for right using while (left < right && nums[right] == nums[right + 1]) right--
- If the sum is greater than 0, move right-- to reduce the sum
- If the sum is less than 0, move left++ to increase the sum
- After the loop, return the result list containing all unique triplets that sum to zero.

```
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res=new ArrayList<>();
        for(int i=0;i<nums.length;i++){
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            int left=i+1;
            int right=nums.length-1;
            while(left<right){
                if(nums[i]+nums[left]+nums[right]==0){
                    res.add(Arrays.asList(nums[i],nums[left],nums[right]));
                    left++;
                    right--;
                    while(left<right && nums[left]==nums[left-1]){
                        left++;
                    }
                    while(left<right && nums[right]==nums[right+1]){
                        right--;
                    }
                }
                else if(nums[i]+nums[left]+nums[right]>0){
                    right--;
                }
                else{
                    left++;
                }
            }
        }
        return res;
        
    }
}
```

- **Time Complexity** - O(N*N)
- **Space Complexity** - O(1)
