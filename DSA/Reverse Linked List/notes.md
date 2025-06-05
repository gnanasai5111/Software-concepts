## Reverse Linked List

Given the head of a singly linked list, reverse the list, and return the reversed list.

```

Example 1:

Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]

Example 2:

Input: head = [1,2]
Output: [2,1]

Example 3:

Input: head = []
Output: []

```

**Constraints** :

- The number of nodes in the list is the range [0, 5000].
- -5000 <= Node.val <= 5000

## Brute Force

- The method reverseList takes the head of a singly linked list and returns the head of the reversed list.
- An ArrayList is used to store the values of the linked list nodes in order.
- A while loop iterates through the original linked list and appends each node's value to the ArrayList.
- A new linked list is constructed in reverse order using the values stored in the ArrayList.
- A for loop starts from the end of the ArrayList and creates new nodes with the stored values.
- The first node created in the loop becomes the new head of the reversed list.
-  Subsequent nodes are linked to the current node to build the reversed list.
- The head of the newly created reversed linked list is returned at the end.

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
    public ListNode reverseList(ListNode head) {
        ArrayList<Integer> list=new ArrayList<>();
        ListNode node=head;
        while(node!=null){
            list.add(node.val);
            node=node.next;
        }
        ListNode curr=null;
        for(int i=list.size()-1;i>=0;i--){
            ListNode newNode=new ListNode(list.get(i));
            if(i==list.size()-1){
                head=newNode;
                curr=newNode;
            }
            else{
                curr.next=newNode;
                curr=newNode;
            }
        }
        return head;
        
    }
}
```

**Time Complexity** - O(N)
**Space Complexity** - O(N)


## Reverse the Pointer

- The method reverseList reverses a singly linked list in-place and returns the new head of the reversed list.
- Two pointers are used: prev (initially null) to keep track of the reversed part, and curr (starting at head) to iterate through the original list.
- A while loop runs until curr becomes null, meaning the end of the list is reached.
- Inside the loop, the next node (curr.next) is stored in a temporary variable next.
- The next pointer of the current node is reversed by pointing it to prev.
- The prev pointer is moved one step forward to curr, and curr is moved to next.
- After the loop, prev points to the new head of the reversed list, which is returned.

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
    public ListNode reverseList(ListNode head) {
        ListNode curr=head;
        ListNode prev=null;
        while(curr!=null){
            ListNode next=curr.next;
            curr.next=prev;
            prev=curr;
            curr=next;
        }
        return prev;
        
    }
}
```

**Time Complexity** - O(N)
**Space Complexity** - O(1)
