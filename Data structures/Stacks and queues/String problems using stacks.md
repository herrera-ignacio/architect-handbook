# String problems using stacks
## Overview
Normally, string questions that can utilize a stack will involve iterating over the string and putting characters into the stack, and comparing the top of the stack with the current character at each iteration.
Stacks are useful for **string matching** because it saves a "history" of the previous characters.
## Examples
### Example: Valid parentheses
Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid. The string is valid if all open brackets are closed by the same type of closing bracket in the correct order, and each closing bracket closes exactly one open bracket.

For example, `s = "({})"` and `s = "(){}[]"` are valid, but `s = "(]"` and `s = "({)}"` are not valid.
#### Solution
The "correct" order is determined by whatever the previous opening bracket was. The order is **last in, first out (LIFO)** - the last opening bracket we saw is the first one we should close, which is perfect functionality for a stack to provide.
As we iterate over the string, if we see an opening bracket, we should put it on the stack. If we see a closing bracket, we can check the most recent unclosed opening bracket by popping it from the top of the stack. If it matches, then continue, if it doesn't, or there is no opening bracket on the stack at all (this would occur in a case like `"{}]"`), then we know the string is invalid. In the end, there should be no unmatched open brackets (like in the case of `"(){"`), so the stack should be empty for the string to be valid.
How can we associate the opening and closing brackets together? We can use a hash map to map each opening bracket to its closing bracket. Then, when we see a closing bracket, we can use the top of the stack as a key and check if the value is equal to the current character.
```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        matching = {"(": ")", "[": "]", "{": "}"}
        
        for c in s:
            if c in matching: # if c is an opening bracket
                stack.append(c)
            else:
                if not stack:
                    return False
                
                previous_opening = stack.pop()
                if matching[previous_opening] != c:
                    return False
 
        return not stack
```

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function(s) {
    let stack = [];
    const matching = {
        "(": ")",
        "[": "]",
        "{": "}"
    }
    
    for (const c of s) {
        if (c in matching) { // if c is an opening bracket
            stack.push(c);
        } else {
            if (!stack.length) {
                return false;
            }
            
            let previousOpening = stack.pop();
            if (matching[previousOpening] != c) {
                return false;
            }
        }
    }
    
    return !stack.length;
};
```
Because the stack's push and pop operations are $O(1)$, this gives us a time complexity of $O(n)$, where $n$ is the size of the input array. This is because each element can only be pushed or popped once. The space complexity is also $O(n)$ because the stack's size can grow linearly with the input size.
### Example: Remove all adjacent duplicates in string
You are given a string `s`. Continuously remove duplicates (two of the same character beside each other) until you can't anymore. Return the final string after this.

For example, given `s = "abbaca"`, you can first remove the `"bb"` to get `"aaca"`. Next, you can remove the `"aa"` to get `"ca"`. This is the final answer.
#### Solution
The tricky part of this problem is that not all removals are necessarily available at the start. As you can see in the example, deleting the `"aa"` is only possible **after** deleting the `"bb"`. We don't need to delete the first character until we have already iterated quite a bit past it
Iterate over the input and put characters in the stack. At each step, if the top of the stack is the same as the current character, we know that they are adjacent (at some point in time) and can be deleted.

```python
class Solution:
    def removeDuplicates(self, s: str) -> str:
        stack = []
        for c in s:
            if stack and stack[-1] == c:
                stack.pop()
            else:
                stack.append(c)
        
        return "".join(stack)
```

```javascript
/**
 * @param {string} s
 * @return {string}
 */
var removeDuplicates = function(s) {
    let stack = [];
    for (const c of s) {
        if (stack.length && stack[stack.length - 1] == c) {
            stack.pop();
        } else {
            stack.push(c);
        }
    }
    
    return stack.join("");
};
```
### Example: Backspace string compare
Given two strings `s` and `t`, return true if they are equal when both are typed into empty text editors. `'#'` means a backspace character.

For example, given `s = "ab#c"` and `t = "ad#c"`, return true. Because of the backspace, the strings are both equal to `"ac"`.
#### Solution
When typing characters, push them onto a stack. Whatever character is at the top of the stack is the most recently typed character, so when we backspace, we can just pop. Make sure to be careful of the edge case where we backspace on an empty string.
```python
class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        def build(s):
            stack = []
            for c in s:
                if c != "#":
                    stack.append(c)
                elif stack:
                    stack.pop()

            return "".join(stack)

        return build(s) == build(t)
```

```javascript
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var backspaceCompare = function(s, t) {
    let build = s => {
        let stack = [];
        for (const c of s) {
            if (c != "#") {
                stack.push(c);
            } else if (stack.length) {
                stack.pop();
            }
        }
        
        return stack.join("");
    }
    
    return build(s) == build(t);
};
```
