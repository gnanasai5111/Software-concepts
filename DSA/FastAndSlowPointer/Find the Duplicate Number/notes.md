## Find the Duplicate Number

- Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive.
- There is only one repeated number in nums, return this repeated number.
- You must solve the problem without modifying the array nums and uses only constant extra space.

```
Example 1:

Input: nums = [1,3,4,2,2]
Output: 2

Example 2:

Input: nums = [3,1,3,4,2]
Output: 3

Example 3:

Input: nums = [3,3,3,3,3]
Output: 3
```

**Constraints**:
- 1 <= n <= 105
- nums.length == n + 1
- 1 <= nums[i] <= n
- All the integers in nums appear only once except for precisely one integer which appears two or more times.

## Brute Force

- Loop through every element in the array using two nested loops
- For each element nums[i], compare it with all elements after it (nums[j])
- If a match is found (nums[i] == nums[j]), that means it's the duplicate → return it immediately
- If no duplicate is found by the end (which shouldn't happen by problem statement), return -1

```
class Solution {
    public int findDuplicate(int[] nums) {
        for(int i=0;i<nums.length;i++){
            for(int j=i+1;j<nums.length;j++){
                if(nums[i]==nums[j]){
                    return nums[i];
                }
            }
        }
        return -1;
        
    }
}
```

**Time complexity** - o(N*N)
**Space complexity** - o(1)

## HashSet :

- Create an empty HashSet to store seen numbers
- Loop through each number in the array
- If the number is already in the set, it's the duplicate → return it
- If not, add it to the set
- If no duplicate is found (shouldn't happen by constraints), return -1

```
class Solution {
    public int findDuplicate(int[] nums) {
        HashSet<Integer> set=new HashSet<>();
        for(int i=0;i<nums.length;i++){
            if(set.contains(nums[i])){
                return nums[i];
            }
            set.add(nums[i]);
        }
        return -1;
        
    }
}
```

**Time complexity** - o(N)
**Space complexity** - o(N)

## Sorting :

- First, sort the array so that duplicate numbers will be next to each other
- Loop from index 1 to n - 1 and compare each number with the one before it
- If two consecutive numbers are equal, return the number as the duplicate
- If no duplicate is found (theoretically shouldn't happen), return -1

```
class Solution {
    public int findDuplicate(int[] nums) {
        Arrays.sort(nums);
        for(int i=1;i<nums.length;i++){
            if(nums[i]==nums[i-1]){
                return nums[i];
            }
        }
        return -1;
        
    }
}
```

**Time complexity** - o(NlogN)
**Space complexity** - o(1)



## Fast and Slow Pointer(Linked list cycle , Flyods Tortoise and hare Algorithm)

Fast - hare 
slow - tortoise

Use a fast and slow pointer. And interate through the array till both fast and slow pointer intersect.

Consider the distance from start to duplicate value is P.And rest of the path from duplicate value is c.
consider the distance from intersection point to duplicate is x.

so for slow pointer = p+c-x
        fast pointer=p+2c-x
    2*slow=fast
    2*(p+c-x)=p+2c-x
    by solving you get p=x
    so that is why we make fast pointer from starting again so that distance between start to duplicate and from intersection to duplicate
    is same

class Solution {
    public int findDuplicate(int[] nums) {
        int slow=nums[0];
        int fast=nums[0];
        do{
            slow=nums[slow];
            fast=nums[nums[fast]];
        }while(slow!=fast);
        fast=nums[0];
        while(slow!=fast){
            slow=nums[slow];
            fast=nums[fast];
        }
        return slow;      
    }
}

**Time complexity** - o(N)
**Space complexity** - o(1)
    
