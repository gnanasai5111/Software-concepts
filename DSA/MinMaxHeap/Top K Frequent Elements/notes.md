## Top K Frequent Elements

- Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

```
Example 1:

Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]

Example 2:

Input: nums = [1], k = 1
Output: [1]
```

**Constraints** :
- 1 <= nums.length <= 105
- -104 <= nums[i] <= 104
- k is in the range [1, the number of unique elements in the array].
- It is guaranteed that the answer is unique.

## Brute Force

- A HashMap is used to count the frequency of each number in the array.
- A custom Pair class is defined with two fields: num (the element) and freq (its frequency).
- Each entry from the map is converted into a Pair object and added to a List.
- The list of pairs is sorted in descending order based on frequency using a custom comparator.
- After sorting, the top k elements (most frequent) are taken from the list and stored in the result array.
- The result array is returned, containing the k most frequent numbers.

```
class Solution {
    class Pair {
        int num;
        int freq;

        Pair(int num, int freq) {
            this.num = num;
            this.freq = freq;
        }
    }
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer,Integer> map=new HashMap<>();
        for(int i=0;i<nums.length;i++){
            map.put(nums[i],map.getOrDefault(nums[i],0)+1);
        }
        List<Pair> list=new ArrayList<>();
        for(Integer i:map.keySet()){
            list.add(new Pair(i,map.get(i)));
        }
        list.sort((a, b) -> b.freq - a.freq);
        int res[]=new int[k];
        for(int i=0;i<k;i++){
            res[i]=list.get(i).num;
        }
        return res;
        
    }
}
```

**Time Complexity** - O(NlogN)
**Space Complexity** - O(N)



## Min Heap

- It uses a HashMap to count the frequency of each unique element in the array.
- The key in the map is the element, and the value is the number of times it appears.
- A PriorityQueue (min heap) is used to keep track of the top k elements by frequency.
- The custom comparator in the priority queue compares elements based on their frequency in the map.
- For each element in the map, it is added to the priority queue. If the size exceeds k, the least frequent element is removed.
- After all elements are processed, the queue contains the k most frequent elements.
- These elements are extracted from the queue in reverse order to form the result array.
- The result array res[] is filled from the end to the beginning by polling from the priority queue.

```
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer,Integer> map=new HashMap<>();
        for(int i=0;i<nums.length;i++){
            map.put(nums[i],map.getOrDefault(nums[i],0)+1);
        }
        PriorityQueue<Integer> pq=new PriorityQueue<>((a,b)->map.get(a)-map.get(b));
        for(Integer i:map.keySet()){
            pq.add(i);
            if(pq.size()>k){
                pq.poll();
            }
        }
        int res[]=new int[k];
        for(int i=k-1;i>=0;i--){
            res[i]=pq.poll();
        }
        return res;
        
    }
}
```

**Time Complexity** - O(N+NlogK)
**Space Complexity** - O(N+K)

