## 234. Palindrome Linked List     

Given the ```head``` of a singly linked list, return ```true``` if it is a palindrome or ```false``` otherwise.   


### Example 1:   

<IMG src="https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg">   

```  
Input: head = [1,2,2,1]
Output: true
```   

### Example 2:    

<IMG src="https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg">    
  
```  
Input: head = [1,2]
Output: false
```    

### Constraints:    

<code>The number of nodes in the list is in the range [1, 10<sup>5</sup>].
0 <= Node.val <= 9
</code>   
  
<br>  
  
## Approach:   
  
* Check if the given head is null or has only one node. If true, return true.
* Initialize slow and fast pointers to the head of the linked list.
* Traverse the linked list with slow and fast pointers. Stop when fast reaches the end or the second last node.
* Reverse the right half of the linked list using the reverseList method.
* Traverse the left and reversed right halves of the linked list with head and slow pointers, respectively. If any node's value does not match, return false.
* Return true if all nodes match.
* The reverseList method reverses a linked list in place and returns the new head of the reversed list.

  
### Code:  
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
    public boolean isPalindrome(ListNode head) {
        if(head==null || head.next==null) {
            return true;
        }
        ListNode slow = head;
        ListNode fast = head;
        
        //find middle of the linkedList
        while(fast.next!=null && fast.next.next!=null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        //Reverse the right half
        slow.next = reverseList(slow.next);

        slow = slow.next;     
        //now, slow is pointing to the first node of right half
        
        while(slow!=null) {
            if(head.val != slow.val)  return false;
            head = head.next;
            slow = slow.next;
        }
        return true;
    }

    public ListNode reverseList(ListNode head) {
        ListNode next = null;
        ListNode pre = null;

        while(head != null) {
            next = head.next;
            head.next = pre;
            pre = head;
            head = next;
        }
        return pre;
    }
}
```   
  
  
### Complexity:    
  
* Time Complexity: O(n)
    * n is the number of nodes in the linked list.
    * Finding middle of linked list, reversing right half, and traversing left and reversed right halves takes n/2 iterations, which simplifies to O(n).

* Space Complexity: O(1)
    * Uses constant space for slow, fast, next, and pre pointers.

