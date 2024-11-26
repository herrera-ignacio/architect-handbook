# Reversing a linked list
## Iterative approach
Imagine that we have a linked list `1 -> 2 -> 3 -> 4`, and we want to return `4 -> 3 -> 2 -> 1`.
1. When we are at a node `curr`, we need to set its `next` pointer to the node we were at previously.
    - Use a `prev` pointer to track the previous node.
2. The prev pointer needs to also update every iteration.
    - After updating `curr.next`, set `prev = curr` in preparation for the next node.
3. If we set `curr.next = prev`, then we lose the reference to the original `curr.next`.
    - Use `nextNode` to keep a reference to the original `curr.next`.
The time complexity is $O(n)$ where $n$ is the number of nodes in the linked list and the space complexity is $O(1)$ as we are only using a few pointers.
## Iterative reversal examples
### C++
```cpp
ListNode* reverseList(ListNode* head) {
    ListNode* prev = nullptr;
    ListNode* curr = head;
    while (curr != nullptr) {
        ListNode* nextNode = curr->next; // first, make sure we don't lose the next node
        curr->next = prev;               // reverse the direction of the pointer
        prev = curr;                     // set the current node to prev for the next node
        curr = nextNode;                 // move on
    }

    return prev;
}
```
### JavaScript
```js
let reverseList = head => {
    let prev = null;
    let curr = head;
    while (curr) {
        let nextNode = curr.next; // first, make sure we don't lose the next node
        curr.next = prev;         // reverse the direction of the pointer
        prev = curr;              // set the current node to prev for the next node
        curr = nextNode;          // move on
    }

    return prev;
}
```
### Python
```python
def reverse_list(head):
    prev = None
    curr = head
    while curr:
        next_node = curr.next # first, make sure we don't lose the next node
        curr.next = prev      # reverse the direction of the pointer
        prev = curr           # set the current node to prev for the next node
        curr = next_node      # move on
        
    return prev
```

## Recursive approach
- Base case: If the `head` is `null` or only one node (`head.next` is `null`), the reversed list is the same as the current list. Return `head`.
- Recursive call: Reverse the rest of the list starting from `head.next`.
- Reverse pointers: After the recursion, set `head.next.next` to point back to `head` (reversing the link). Set `head.next` to `null` to break the current forward link.
- Return the new head.
```js
var reverseList = function(head) {
  // Base case: if the list is empty or only one node, return it
  if (!head || !head.next) {
    return head;
  }

  // Recursively reverse the rest of the list
  const newHead = reverseList(head.next);

  // Reverse the current node's pointer
  head.next.next = head;
  head.next = null;

  // Return the new head of the reversed list
  return newHead;
};
```
## Examples
### Example: Maximum twin sum of a linked list
[2130. Maximum Twin Sum of a Linked List](https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list/) asks for the maximum pair sum. The pairs are the first and last node, second and second last node, third and third last node, etc..
The trivial solution would be to convert the linked list into an array, that way you can access the pairs easily by indexing. The more elegant $O(1)$ space solution is as follows:
1. Find the middle of the linked list using the fast and slow pointer technique from the previous article.
2. Once at the middle of the linked list, perform a reversal. Basically, reverse only the second half of the list.
3. After reversing the second half, every node is spaced `n / 2` apart from its pair node, where `n` is the number of nodes in the list which we can find from step 1.
4. With that in mind, create another fast pointer `n / 2` ahead of `slow`. Now, just iterate `n / 2` times from `head` to find every pair sum `slow.val + fast.val`.

> [!tip]
> Unlike the previous examples, the reversal is not the entire point of the problem, but just a tool used to arrive at a better solution.
### Example: Swap nodes in pairs
Given the `head` of a linked list, swap every pair of nodes. For example, given a linked list `1 -> 2 -> 3 -> 4 -> 5 -> 6`, return a linked list `2 -> 1 -> 4 -> 3 -> 6 -> 5`.
1. Performs an edge swap from `A -> B -> C -> ...` to `A <-> B C -> ...`.
2. Make sure we can still access the rest of the list beyond the current pair (saves `C`).
3. Now that `A <-> B` is isolated from the rest of the list, save a pointer to `A` to connect it with the rest of the list later. Move to the next pair.
4. Connect the previous pair to the rest of the list. In this case connecting `A -> D`.
5. Use a dummy pointer to keep a reference to what we want to return.
6. Handle the case when there's an odd number of nodes.

> [!tip]
> The order of the steps here is not chronological. It's just an order that we might think of when we are trying to consider the requirements of the problem.
#### JavaScript
```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var swapPairs = function(head) {
    // Check edge case: linked list has 0 or 1 nodes, just return
    if (!head || !head.next) {
        return head;
    }
    
    let dummy = head.next;              // Step 5
    let prev = null;                    // Initialize for step 3
    while (head && head.next) {
        if (prev) {
            prev.next = head.next;      // Step 4
        }
        prev = head;                    // Step 3
        
        let nextNode = head.next.next;  // Step 2
        head.next.next = head;          // Step 1
        
        head.next = nextNode;           // Step 6
        head = nextNode;                // Move to next pair (Step 3)
    }
    
    return dummy;
};
```
#### Python
```python
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        # Check edge case: linked list has 0 or 1 nodes, just return
        if not head or not head.next:
            return head

        dummy = head.next               # Step 5
        prev = None                     # Initialize for step 3
        while head and head.next:
            if prev:
                prev.next = head.next   # Step 4
            prev = head                 # Step 3

            next_node = head.next.next  # Step 2
            head.next.next = head       # Step 1

            head.next = next_node       # Step 6
            head = next_node            # Move to next pair (Step 3)

        return dummy
```