## Kth Largest Element in an Array

- Given an integer array nums and an integer k, return the kth largest element in the array.
- Note that it is the kth largest element in the sorted order, not the kth distinct element.
- Can you solve it without sorting?

```
Example 1:

Input: nums = [3,2,1,5,6,4], k = 2
Output: 5

Example 2:

Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
```

**Constraints** :
- 1 <= k <= nums.length <= 105
- -104 <= nums[i] <= 104

## Brute Force :

```
class Solution {
    public int findKthLargest(int[] nums, int k) {
        Arrays.sort(nums);
        return nums[nums.length-k];
    }
}
```

- Arrays.sort(nums) sorts the array in ascending order.
- In a sorted array, the kth largest element is at the index nums.length - k

**Time Complexity** - O(NlogN)
**Space Complexity** - O(1)

## MinHeap

- It uses a PriorityQueue which acts as a min heap by default in Java.
- All elements from the array are added one by one into the priority queue.
- If the heap size exceeds k, the smallest element is removed using poll().
- This ensures that the heap always contains the k largest elements seen so far.
- After all elements are processed, the top of the heap (peek()) is the kth largest element.

```
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> pq=new PriorityQueue<>();
        for(int i=0;i<nums.length;i++){
            pq.add(nums[i]);
            if(pq.size()>k){
                pq.poll();
            }
        }
        return pq.peek();
    }
}
```

**Time Complexity** - O(NlogK)
**Space Complexity** - O(K)
