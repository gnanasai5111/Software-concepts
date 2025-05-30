##  Happy Number

- Given head, the head of a linked list, determine if the linked list has a cycle in it.
- There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer.
- Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.
- Return true if there is a cycle in the linked list. Otherwise, return false.

```
Example 1:
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

Example 2:

Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.

Example 3:

Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
```
 
**Constraints**:

- The number of the nodes in the list is in the range [0, 104].
- -105 <= Node.val <= 105
- pos is -1 or a valid index in the linked-list.


## Brute Force :

- Uses HashSet to track visited nodes during traversal
- Starts from head and checks each node one by one
- If a node is already in the set, a cycle exists and returns true
- If traversal ends (node becomes null), returns false indicating no cycle

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
        ListNode node=head;
        HashSet<ListNode> set=new HashSet<>();
        while(node!=null){
            if(set.contains(node)){
                return true;
            }
            set.add(node);
            node=node.next;
        }
        return false;
        
    }
}
```

- **Time Complexity** - O(N)
- **Space Complexity** - O(N)


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
