##  Swap Nodes in Pairs

- Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

```
Example 1:
Input: head = [1,2,3,4]
Output: [2,1,4,3]

Example 2:

Input: head = []
Output: []

Example 3:

Input: head = [1]
Output: [1]

Example 4:

Input: head = [1,2,3]
Output: [2,1,3]
```
 
**Constraints**:

- The number of nodes in the list is in the range [0, 100].
- 0 <= Node.val <= 100


## Brute Force :

- Starts from the head and traverses the list in pairs
- For each pair, stores reference to the next node
- Swaps the values of the current node and the next node
- Moves the pointer two steps ahead to skip the swapped pair
- Handles edge cases where list has odd number of nodes

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode curr=head;
        ListNode next=null;
        while(curr!=null && curr.next!=null){
            next=curr.next;
            if(next!=null){
                int val=curr.val;
                curr.val=next.val;
                next.val=val;
            }
            curr=curr.next.next;

        }
        return head;
        
    }
}
```

- **Time Complexity** - O(N)
- **Space Complexity** - O(1)


## Fast and Slow Pointer (Floyd’s Cycle Detection approach (also known as Tortoise and Hare))

- Checks if list is empty or has only one node — in which case, no cycle
- Uses two pointers: slow moves one step, fast moves two steps
- If slow and fast ever meet, a cycle exists and returns true
- If fast or fast.next becomes null, list ends and has no cycle


```
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head==null || head.next==null){
            return false;
        }
        ListNode slow=head;
        ListNode fast=head.next;
        while(fast!=null && fast.next!=null){
            if(slow==fast){
                return true;
            }
            slow=slow.next;
            fast=fast.next.next;
        }
        return false;
        
    }
}
```

- **Time Complexity** - O(N)
- **Space Complexity** - O(1)
