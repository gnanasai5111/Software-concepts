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


## Swapping Node using Previous values

- The function swaps every two adjacent nodes in a singly linked list.
- A dummy node is created to simplify edge case handling, especially when the head is involved in a swap.
- dummy.next = head connects the dummy node to the start of the list.
- prev is initialized to point to the dummy node; it tracks the node before the current pair.
- first starts at the head and represents the first node in the current pair.
- In each iteration of the loop, the function checks if there are at least two nodes left to swap.
- second = first.next identifies the second node in the pair.
- first.next = second.next skips over second to prepare for the swap.
- second.next = first completes the swap by pointing second to first.
- prev.next = second connects the previous part of the list to the newly swapped pair.
- prev = first moves the prev pointer forward to the last node of the swapped pair.
- first = first.next moves the first pointer forward to the next node to be processed.
- The loop continues until no more pairs are left to swap.
- The function returns dummy.next, which points to the new head of the swapped list.


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
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode prev = dummy;
        ListNode first=head;
        ListNode second=null;
        while(first!=null && first.next!=null){
            second=first.next;
            first.next=second.next;
            second.next=first;
            prev.next=second;
            prev=first;
            first=first.next;
        }
        return dummy.next;       
    }
}
```

- **Time Complexity** - O(N)
- **Space Complexity** - O(1)



