## Reverse Linked List II

- Given the head of a singly linked list and two integers left and right where left <= right, reverse the nodes of the list from position left to position right, and return the reversed list.

```
Example 1:


Input: head = [1,2,3,4,5], left = 2, right = 4
Output: [1,4,3,2,5]

Example 2:

Input: head = [5], left = 1, right = 1
Output: [5]
```

**Constraints** :
- The number of nodes in the list is n.
- 1 <= n <= 500
- -500 <= Node.val <= 500
- 1 <= left <= right <= n

## Iterative approach 

- This method reverses a portion of a singly linked list from position left to right (1-based index).
- It handles edge cases where the list is empty or has only one node.
- It uses a pointer curr to traverse the list up to the left position.
- The node before the reversal starts is stored in start.
- The node at position left is stored in end, which becomes the tail of the reversed segment.
- The reversal is done using a loop that reverses pointers between left and right using prev, curr, and next.
- After reversal, if start is not null, it connects start.next to the new head of the reversed part (prev).
- If left is 1, start is null, so the list head is updated to prev.
- The original end node is connected to the node following the reversed segment using end.next = curr.
- The updated list head is returned.

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
    public ListNode reverseBetween(ListNode head, int left, int right) {
        if(head==null || head.next==null){
            return head;
        }
        int i=1;
        ListNode curr=head;
        ListNode start=null;
        while(i<left){
            start=curr;
            curr=curr.next;
            i++;
        }
        ListNode end=curr;
        ListNode prev=null;
        for(i=left;i<=right;i++){
            ListNode next=curr.next;
            curr.next=prev;
            prev=curr;
            curr=next;
        }
        if (start != null) {
            start.next = prev;
        } else {
            head = prev;
        }
        end.next=curr;
        return head;   
    }
}
```

**Time Complexity** - O(N)
**Space Complexity** - O(1)
