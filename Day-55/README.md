## 206. Reverse Linked List   

Given the **head** of a singly linked list, reverse the list, and return the reversed list.   

### Example 1:   
```
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```   

### Example 2:  
```
Input: head = [1,2]
Output: [2,1]
```  

### Example 3:  
```
Input: head = []
Output: []
```   

### Constraints:  
```
The number of nodes in the list is the range [0, 5000].
-5000 <= Node.val <= 5000
```  

<br>  

## Approach:  

* Create a variable(ListNode object) "prev" and initialize it to null.
* Create a variable "current" and initialize it to the head of the input list.
* Use a while loop to iterate through the list, stopping when "current" is null.
* In each iteration, create a variable "next" and set it to the value of "current.next".
* Set "current.next" to the value of "prev".
* Set "prev" to the value of "current".
* Set "current" to the value of "next".
* Return "prev" as the new head of the reversed list.  

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
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode current = head;

        while(current != null) { 
            ListNode next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }
        return prev;
    }
}
```  

### Complexity:  

* Time Complexity: O(n)   
    * n is number of nodes in the input list. 
    * Iterates through each node in the list once.   

* Space Complexity: O(1)  
    * Uses constant amount of memory to store "prev", "current", and "next".

