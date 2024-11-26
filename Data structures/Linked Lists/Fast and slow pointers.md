# Fast and slow pointers
## Overview
It's an implementation of the [[Two pointers]] technique. The idea is to have two pointers that don't move side by side (i.e., they move at different "speeds" during iteration, begin iteration from different locations, or any other difference).
Usually the "fast" pointer moves two nodes per iteration, whereas the "slow" pointer moves one node per iteration.
```
// head is the head node of a linked list
function fn(head):
    slow = head
    fast = head

    while fast and fast.next:
        Do something here
        slow = slow.next
        fast = fast.next.next
```
## Examples
### Example: Return the value of the node in the middle when odd number of nodes
For example, given a linked list that represents `1 -> 2 -> 3 -> 4 -> 5`, return `3`.
You could convert it to an array but let's just assume we don't want to allocate additional space. 
We could iterate through the linked list once to find the length, then iterate from the head again once we know the length to find thew middle.
```cpp
int getMiddle(ListNode* head) {
    int length = 0;
    ListNode* dummy = head;
    while (dummy != nullptr) {
        length++;
        dummy = dummy->next;
    }

    for (int i = 0; i < length / 2; i++) {
        head = head->next;
    }

    return head->val;
}
```
The most elegant solution comes with the fast and slow pointers technique. If you have a pointer moving twice as fast as the other, then by the time it reaches the end, the slow pointer will be halfway through.
```cpp
int getMiddle(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
    }

    return slow->val;
}
```
The time complexity is still $O(n)$ but the pointers use $O(1)$ space.
### Example: Linked List Cycle
Given the `head` of a linked list, determine if the linked list has a cycle.
There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer.
Move a fast pointer twice the speed of a slow pointer so that if they ever meet (except at the start), there there must be a cycle. If the fast pointer reaches the end of the linked list, then there isn't a cycle.
```cpp
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode* slow = head;
        ListNode* fast = head;
        while (fast != nullptr && fast->next != nullptr) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) {
                return true;
            }
        }
        
        return false;
    }
};
```
This approach gives us a time complexity of $O(n)$ and a space complexity of $O(1)$, where `n` is the number of nodes in the linked list. Note that this problem can also be solved using hashing, although it would require $O(n)$ space.
```cpp
class Solution {
public:
    bool hasCycle(ListNode *head) {
        unordered_set<ListNode*> seen;
        while (head != nullptr) {
            if (seen.find(head) != seen.end()) {
                return true;
            }
            seen.insert(head);
            head = head->next;
        }
        
        return false;
    }
};
```
### Example: Return the kth node from the end
For example, given the linked list that represents `1 -> 2 -> 3 -> 4 -> 5` and `k = 2`, return the node with value `4`, as it is the 2nd node from the end.
If we separate the two pointers by a gap of `k`, and then move them at the same speed, they will always be `k` apart. When the fast pointer (the one further ahead) reaches the end, then the slow pointer must be at the desired node, since it is `k` nodes behind.
```cpp
ListNode* findNode(ListNode* head, int k) {
    ListNode* slow = head;
    ListNode* fast = head;
    for (int i = 0; i < k; i++) {
        fast = fast->next;
    }

    while (fast != nullptr) {
        slow = slow->next;
        fast = fast->next;
    }
    
    return slow;
}
```
For the same reasons as in the first example, the time complexity of this algorithm is $O(n)$ and the space complexity is $O(1)$, where nn is the number of nodes in the linked list.