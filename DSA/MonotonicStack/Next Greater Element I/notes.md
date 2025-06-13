## Next Greater Element I

- The next greater element of some element x in an array is the first greater element that is to the right of x in the same array.
- You are given two distinct 0-indexed integer arrays nums1 and nums2, where nums1 is a subset of nums2.
- For each 0 <= i < nums1.length, find the index j such that nums1[i] == nums2[j] and determine the next greater element of nums2[j] in nums2. If there is no next greater element, then the answer for this query is -1.
- Return an array ans of length nums1.length such that ans[i] is the next greater element as described above.

```
Example 1:

Input: nums1 = [4,1,2], nums2 = [1,3,4,2]
Output: [-1,3,-1]
Explanation: The next greater element for each value of nums1 is as follows:
- 4 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
- 1 is underlined in nums2 = [1,3,4,2]. The next greater element is 3.
- 2 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.

Example 2:

Input: nums1 = [2,4], nums2 = [1,2,3,4]
Output: [3,-1]
Explanation: The next greater element for each value of nums1 is as follows:
- 2 is underlined in nums2 = [1,2,3,4]. The next greater element is 3.
- 4 is underlined in nums2 = [1,2,3,4]. There is no next greater element, so the answer is -1.
```

**Constraints**:
- 1 <= nums1.length <= nums2.length <= 1000
- 0 <= nums1[i], nums2[i] <= 104
- All integers in nums1 and nums2 are unique.
- All the integers of nums1 also appear in nums2.

## Brute Force

- For each element in nums1, find its index in nums2
- If the element is not found in nums2, set result as -1
- Otherwise, search to the right in nums2 for the next greater element
- If found, assign it to result; otherwise, keep -1

```
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        int res[]=new int[nums1.length];
        for(int i=0;i<nums1.length;i++){
            int idx=-1;
            for(int j=0;j<nums2.length;j++){
                if(nums1[i]==nums2[j]){
                    idx=j;
                    break;
                }
            }
            if(idx==-1){
                res[i]=-1;
                continue;
            }
            res[i]=-1;
            for(int j=idx+1;j<nums2.length;j++){
                if(nums2[j]>nums1[i]){
                    res[i]=nums2[j];
                    break;
                }
            }

        }
        return res;
        
    }
}
```

**Time complexity** - O(M*N)
**Space Complexity** - O(M)


## Monotonic stack 

- Solves the Next Greater Element I problem using a monotonic stack
- Iterates nums2 from right to left to build a map of each element to its next greater element
- Uses a stack to maintain decreasing elements; pops smaller elements until the next greater is found
- If the stack is empty, no greater element exists, so stores -1
- Pushes the current element onto the stack after processing
- Builds a hashmap mapping each nums2[i] to its next greater element
- For each element in nums1, looks up the precomputed next greater value from the map

```
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        Stack<Integer> st=new Stack<>();
        int res[]=new int[nums1.length];
        HashMap<Integer,Integer> map=new HashMap<>();
        for(int i=nums2.length-1;i>=0;i--){
            while(!st.isEmpty() && nums2[i]>st.peek()){
                st.pop();
            }
            map.put(nums2[i], st.isEmpty() ? -1 : st.peek());
            st.push(nums2[i]);   
        }
        for(int i=0;i<nums1.length;i++){
            res[i]=map.get(nums1[i]);
        }
        return res;
        
    }
}
```

**Time complexity** - O(M+N)
**Space Complexity** - O(M+N)
