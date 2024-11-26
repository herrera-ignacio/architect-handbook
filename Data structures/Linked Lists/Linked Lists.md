# Linked Lists
## Definition
A linked list is similar to an array. It stores data in an ordered manner, but it is implemented using *node* objects. Each node will have a "next" pointer, which points to the node representing the next element in the sequence.
## Example implementation
### JavaScript
```js
class ListNode {
    constructor(val) {
        this.val = val;
        this.next = null;
    }
}

(function main() {
    let one = new ListNode(1);
    let two = new ListNode(2);
    let three = new ListNode(3);
    one.next = two;
    two.next = three;
    let head = one;
    
    console.log(head.val);
    console.log(head.next.val);
    console.log(head.next.next.val);
}());
```
### Python
```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None
    
one = ListNode(1)
two = ListNode(2)
three = ListNode(3)
one.next = two
two.next = three
head = one

print(head.val)
print(head.next.val)
print(head.next.next.val)
```
### C++
```cpp
struct LinkedListNode {
    int val;
    LinkedListNode *next;
    LinkedListNode(int val): val (val), next(nullptr) {}
};

int main() {
    LinkedListNode* one = new LinkedListNode(1);
    LinkedListNode* two = new LinkedListNode(2);
    LinkedListNode* three = new LinkedListNode(3);
    one->next = two;
    two->next = three;
    LinkedListNode* head = one;
    
    cout << head->val << endl;
    cout << head->next->val << endl;
    cout << head->next->next->val << endl;
}
```
## Advantages over array
- You can add/remove elements at any position in $O(1)$.
- The caveat is that you need to have a reference to a node at the position in which you want to perform the operation, otherwise it's $O(n)$. However, this is still much better than a normal (dynamic) array, which requires $O(n)$ for adding and removing from an *arbitrary* position.
- No fixed size. While arrays can be resized, under the hood they still are allocated a fixed size and resizing is expensive.
## Disadvantages over array
- No random access. Therefore, it requires $O(n)$ to access an element at a given position while an array has $O(1)$.
- More overhead than arrays - every element needs to have extra storage for the pointers. If you are only storing small items like booleans or characters, then you may be more than doubling the space needed.
## Mechanics
Understanding how to manipulate linked list nodes and pointers using code is essential.
### Assignment (=)
When you assign a pointer to an existing linked list node, the pointer refers to the object in memory.
```cpp
ListNode* ptr = head;
head = head->next;
head = nullptr;
```
At the end, `ptr` still refers to the original `head` node, even though the `head` variable changed. Variables remain at nodes unless they are modified directly (i.e., `ptr = something` is the only way to modify `ptr`).
### Chaining .next
If you have multiple `next`, everything before the final `.next` refers to one node.
For example, given a linked list `1 -> 2 -> 3`, if you have `head` pointing at the first node, and you do `head.next.next`, you are actually referring to `2.next`, because `head.next` is the `2`.
### Traversal
Iterating forward through a linked list can be done with a simple loop.
```cpp
int getSum(ListNode* head) {
    int ans = 0;
    while (head != nullptr) {
        ans += head->val;
        head = head->next;
    }

    return ans;
}
```
Also, it can be done recursively.
```cpp
int getSum(ListNode* head) {
    if (head == nullptr) {
        return 0;
    }

    return head->val + getSum(head->next);
}
```
### Dummy pointers
Sometimes, it's better to traverse using a "dummy" pointer and to keep `head` at the head.
```cpp
int getSum(ListNode* head) {
    int ans = 0;
    ListNode* dummy = head;
    while (dummy != nullptr) {
        ans += dummy->val;
        dummy = dummy->next;
    }

    // same as before, but we still have a pointer at the head
    return ans;
}
```
## Types
### Singly linked list
Each node only has a pointer to the `next` node. This means you can only move forward in the list when iterating.
```cpp
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int val) : val(val), next(nullptr) {}
};

// Let prevNode be the node at position i - 1
void addNode(ListNode* prevNode, ListNode* nodeToAdd) {
    nodeToAdd->next = prevNode->next;
    prevNode->next = nodeToAdd;
}

// Let prevNode be the node at position i - 1
void deleteNode(ListNode* prevNode) {
    prevNode->next = prevNode->next->next;
}
```
If you have a reference to the node at `i - 1`, then insertion and deletion are $O(1)$. If not, you need to obtain the reference by iterating from the head, which for an arbitrary position is $O(n)$.
### Doubly linked list
Each node has a pointer to both the `next` and `prev` node. This means you can iterate in both directions.
For operations, we need to do extra work to also update the `prev` pointers.
```cpp
struct ListNode {
    int val;
    ListNode *next;
    ListNode *prev;
    ListNode(int val) : val(val), next(nullptr), prev(nullptr) {}
};

// Let node be the node at position i
void addNode(ListNode* node, ListNode* nodeToAdd) {
    ListNode* prevNode = node->prev;
    nodeToAdd->next = node;
    nodeToAdd->prev = prevNode;
    prevNode->next = nodeToAdd;
    node->prev = nodeToAdd;
}

void deleteNode(ListNode* node) {
    ListNode* prevNode = node->prev;
    ListNode* nextNode = node->next;
    prevNode->next = nextNode;
    nextNode->prev = prevNode;
}
```
### Linked lists with sentinel nodes
Sentinel nodes sit at the start (`head`) and end (`tail`) of linked lists and are used to make operations and the code needed to execute those operations cleaner.
Even if there are no nodes, you still keep pointers to a `head` and `tail`. Then, the real head is `head.next` and the real tail is `tail.prev` (i.e., the sentinel nodes are not part of our linked list).
The sentinel nodes also allow us to easily add and remove from the front or back of the linked list in $O(1)$.
```cpp
struct ListNode {
    int val;
    ListNode *next;
    ListNode *prev;
    ListNode(int val) : val(val), next(nullptr), prev(nullptr) {}
};

void addToEnd(ListNode* nodeToAdd) {
    nodeToAdd->next = tail;
    nodeToAdd->prev = tail->prev;
    tail->prev->next = nodeToAdd;
    tail->prev = nodeToAdd;
}

void removeFromEnd() {
    if (head->next == tail) {
        return;
    }

    ListNode* nodeToRemove = tail->prev;
    nodeToRemove->prev->next = tail;
    tail->prev = nodeToRemove->prev;
}

void addToStart(ListNode* nodeToAdd) {
    nodeToAdd->prev = head;
    nodeToAdd->next = head->next;
    head->next->prev = nodeToAdd;
    head->next = nodeToAdd;
}

void removeFromStart() {
    if (head->next == tail) {
        return;
    }

    ListNode* nodeToRemove = head->next;
    nodeToRemove->next->prev = head;
    head->next = nodeToRemove->next;
}

ListNode* head = new ListNode(-1);
ListNode* tail = new ListNode(-1);
head->next = tail;
tail->prev = head;
```