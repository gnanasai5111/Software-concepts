## Sort an Array

- Given an array of integers nums, sort the array in ascending order and return it.

```
Example 1:

Input: nums = [5,2,3,1]
Output: [1,2,3,5]
Explanation: After sorting the array, the positions of some numbers are not changed (for example, 2 and 3), while the positions of other numbers are changed (for example, 1 and 5).

Example 2:

Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
Explanation: Note that the values of nums are not necessairly unique.
```

**Constraints**:
- 1 <= nums.length <= 5 * 104
- -5 * 104 <= nums[i] <= 5 * 104

## Bubble Sort 

- This solution uses the Bubble Sort algorithm to sort the array in ascending order.
- It uses two nested loops: the outer loop controls the number of passes, and the inner loop compares adjacent elements.
- If the current element is greater than the next one, they are swapped to move the larger element toward the end.
- After each full inner loop pass, the largest unsorted element reaches its correct position at the end.
- The process continues until the array is fully sorted.

```
class Solution {
    public int[] sortArray(int[] nums) {
        for(int i=0;i<nums.length;i++){
            for(int j=0;j<nums.length-i-1;j++){
                if(nums[j]>nums[j+1]){
                    int temp=nums[j];
                    nums[j]=nums[j+1];
                    nums[j+1]=temp;
                }
            }
        }
        return nums;
        
    }
}
```

- **Time Complexity** - O(N*N)
- **Space Complexity** - O(1)

## Selection Sort

- This solution uses the Selection Sort algorithm to sort the array in ascending order.
- It maintains two parts in the array: the sorted part at the beginning and the unsorted part at the end.
- For each index i, it finds the index of the smallest element in the unsorted part and stores it in min.
- If the smallest element is not already at index i, it swaps the current element with the minimum element.
- This ensures that the smallest remaining element is placed at its correct position in each pass.

```
class Solution {
    public int[] sortArray(int[] nums) {
        for(int i=0;i<nums.length;i++){
            int min=i;
            for(int j=i+1;j<nums.length;j++){
                if(nums[j]<nums[min]){
                    min=j;
                }
            }
            if(min!=i){
                int temp=nums[i];
                nums[i]=nums[min];
                nums[min]=temp;
            }
        }
        return nums;      
    }
}
```

- **Time Complexity** - O(N*N)
- **Space Complexity** - O(1)

## Insertion Sort

- This code uses Insertion Sort to sort the array in increasing order.
- It starts from the second element and goes one by one to the end.
- Each time, it takes the current number and compares it with numbers before it.
- If the current number is smaller, it keeps swapping it left until it finds the right place.
- It works like how we sort playing cards in hand.

```
class Solution {
    public int[] sortArray(int[] nums) {
        for(int i=1;i<nums.length;i++){
           for(int j=i;j>=1;j--){
                if(nums[j]<nums[j-1]){
                    int temp=nums[j];
                    nums[j]=nums[j-1];
                    nums[j-1]=temp;
                }
           }
        }
        return nums;      
    }
}
```

- **Time Complexity** - O(N*N)
- **Space Complexity** - O(1)

## Counting sort 

- This code implements counting sort that handles both positive and negative integers by shifting indices based on the minimum value.
- It first finds the minimum and maximum values in the input array to determine the range of numbers.
- A count array of size max - min + 1 is created to store frequencies of all numbers in the range, including negatives shifted by subtracting min.
- The frequency of each number is recorded by incrementing the count at nums[i] - min.
- The sorted array is reconstructed by iterating over the count array and placing each number back into the original array according to its frequency, adjusting the index by adding min


```
class Solution {
    public int[] sortArray(int[] nums) {
        int max = nums[0];
        int min = nums[0];

        for (int i = 0; i < nums.length; i++) {
            max = Math.max(max, nums[i]);
            min = Math.min(min, nums[i]);
        }

        int[] count = new int[max - min + 1];

        for (int i = 0; i < nums.length; i++) {
            count[nums[i] - min]++;
        }

        int index = 0;
        for (int i = 0; i < count.length; i++) {
            while (count[i] > 0) {
                nums[index++] = i + min;
                count[i]--;
            }
        }

        return nums;
    }
}
```

- **Time Complexity** - O(n + k) where k=(max - min + 1)
- **Space Complexity** - O(k)

## Merge Sort 

- Uses Divide and Conquer strategy.
- Recursively splits the array into halves until single elements remain.
- Merges the sorted halves back while maintaining order.
- mergeSort(left, right, nums) recursively sorts subarrays.
- merge(left, mid, right, nums) merges two sorted subarrays into one.
- Uses a temporary array merged[] to hold sorted elements during merge.
- Copies merged results back into the original nums[] array.
- Ensures stable sort (does not change relative order of equal elements).

```
class Solution {
    public void merge(int left, int mid, int right, int[] nums) {
        int pointer1 = left;
        int pointer2 = mid + 1;
        int[] merged = new int[right - left + 1];
        int index = 0;

        while (pointer1 <= mid && pointer2 <= right) {
            if (nums[pointer1] <= nums[pointer2]) {
                merged[index++] = nums[pointer1++];
            } else {
                merged[index++] = nums[pointer2++];
            }
        }

        while (pointer1 <= mid) {
            merged[index++] = nums[pointer1++];
        }

        while (pointer2 <= right) {
            merged[index++] = nums[pointer2++];
        }

        for (int i = 0; i < merged.length; i++) {
            nums[left + i] = merged[i];
        }
    }

    public void mergeSort(int left, int right, int[] nums) {
        if (left >= right) return;

        int mid = left + (right - left) / 2;
        mergeSort(left, mid, nums);
        mergeSort(mid + 1, right, nums);
        merge(left, mid, right, nums);
    }

    public int[] sortArray(int[] nums) {
        mergeSort(0, nums.length - 1, nums);
        return nums;
    }
}
```

- **Time Complexity** - O(NlogN) 
- **Space Complexity** - O(N)

## Quick Sort 

- Uses QuickSort algorithm to sort an array in-place
- partition function chooses the first element as pivot
- Two pointers i and j traverse the array from left and right respectively
- Pointer i moves right while elements are less than or equal to pivot
- Pointer j moves left while elements are greater than pivot
- When i is less than j, elements at i and j are swapped
- After the pointers cross, pivot is swapped with element at j to place it correctly
- partition returns the final pivot index
- quickSort recursively sorts subarrays before and after the pivot
- sortArray calls quickSort on the whole array and returns the sorted array

```
class Solution {
    public int partition(int l,int r,int nums[]){
        int pivot=nums[l];
        int i=l;
        int j=r;
        while(i<j){
            while(nums[i]<=pivot && i<=r-1){
                i++;
            }
            while(nums[j]>pivot && j>=l+1){
                j--;
            }
            if(i<j){
                int temp=nums[i];
                nums[i]=nums[j];
                nums[j]=temp;
            }
        }
        nums[l]=nums[j];
        nums[j]=pivot;
        return j;
    }
    public void quickSort(int l,int r,int nums[]){
        if(l<r){
            int partitionIndex=partition(l,r,nums);
            quickSort(l,partitionIndex-1,nums);
            quickSort(partitionIndex+1,r,nums);
        }
    }
    public int[] sortArray(int[] nums) {
        quickSort(0,nums.length-1,nums);
        return nums;
        
    }
}
```

- **Time Complexity** - O(NlogN) 
- **Space Complexity** - O(1)


##  Heap

- A heap is a special kind of binary tree used mainly for implementing priority queues and heap sort.
- Its a Complete Binary Tree : All levels are completely filled except possibly the last, which is filled from left to right.
- Max-Heap: Parent node is greater than or equal to its children.
- Min-Heap: Parent node is less than or equal to its children.

## Heap Sort insertion based

- This code sorts an array using Heap Sort.
- A max heap is built using an ArrayList.
- The insert function adds numbers and maintains the max heap by pushing larger numbers up.
- The heapify function fixes the heap by pushing smaller numbers down to the right position.
- After building the heap, the largest number is placed at the end of the array.
- The top element is swapped with the last, and heapify is used to fix the remaining heap.
- This continues until the whole array is sorted in ascending order.
- Sorting happens in the original array, but an ArrayList is used to build the heap.

```
class Solution {
    public void swap(ArrayList<Integer> heap,int i, int j){
        int temp=heap.get(i);
        heap.set(i,heap.get(j));
        heap.set(j,temp);
    }
    public void insert(ArrayList<Integer> heap,int val){
        heap.add(val);
        int index=heap.size()-1;
        while(index>=0){
            int parent=(index-1)/2;
            if(heap.get(index)>heap.get(parent)){
                swap(heap,index,parent);
                index=parent;
            }
            else{
                break;
            }
        }
    }
    public void heapify(ArrayList<Integer> heap,int index, int size){
        int largest=index;
        int left=2*index+1;
        int right=2*index+2;
       if(left<size && heap.get(largest)<heap.get(left)){
            largest=left;
       }
       if(right<size && heap.get(largest)<heap.get(right)){
            largest=right;
       }
       if(largest!=index){
            swap(heap,largest,index);
            heapify(heap,largest,size);
       }
    }
    public int[] sortArray(int[] nums) {
        ArrayList<Integer> heap=new ArrayList<>();
        for(int i=0;i<nums.length;i++){
            insert(heap,nums[i]);
        }
        for(int i=heap.size()-1;i>=0;i--){
            nums[i]=heap.get(0);
            heap.set(0,heap.get(i));
            heapify(heap,0,i);
        }
        return nums;
        
    }
}
```
- **Time Complexity** - O(NlogN)+O(NlogN) 
- **Space Complexity** - O(N)

## Heap Sort (In-place / Efficient Version)

- This code sorts an array using the Heap Sort algorithm.
- heapify() ensures the max-heap property: parent is larger than children.
- In the first loop, we build a max heap by calling heapify() from bottom non-leaf nodes to the root.
- The range starts from nums.length - 1 down to 0, but ideally it should start from nums.length / 2 - 1.
- In the second loop, we repeatedly move the maximum (root at index 0) to the end of the array.
- After swapping the max element with the last, we reduce the heap size and call heapify() on the root to fix the heap.
- The swap() method exchanges two elements in the array.
- This sorts the array in-place without using extra space.

```
class Solution {
    public void swap(int nums[],int i, int j){
        int temp=nums[i];
        nums[i]=nums[j];
        nums[j]=temp;
    }
    public void heapify(int nums[],int index,int size){
        int largest=index;
        int left=2*index+1;
        int right=2*index+2;
       if(left<size && nums[largest]<nums[left]){
            largest=left;
       }
       if(right<size && nums[largest]<nums[right]){
            largest=right;
       }
       if(largest!=index){
            swap(nums,largest,index);
            heapify(nums,largest,size);
       }
    }
    public int[] sortArray(int[] nums) {
        for(int i=nums.length/2-1;i>=0;i--){
            heapify(nums,i,nums.length);
        }
        for(int i=nums.length-1;i>=0;i--){
            swap(nums, 0, i);
            heapify(nums,0,i);
        }
        return nums;
        
    }
}
```

- **Time Complexity** - O(NlogN)
- **Space Complexity** - O(1)
