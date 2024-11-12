# Two pointers
## Overview
Two pointers is an extremely common technique used to solve array and string problems. It involves having two integer variables that both move along an iterable.

> [!tip]
> Two pointers help us cover a sub-array within the main array.

 This means we will have two integers, usually named something like `i` and `j`, or `left` and `right` which each represent an index of the array or string.
## Approach 1: Start from edges
 Start the pointers at the edges of the input. Move them towards each other until they meet.
```
function fn(arr):
    left = 0
    right = arr.length - 1

    while left < right:
        Do some logic here depending on the problem
        Do some more logic here to decide on one of the following:
            1. left++
            2. right--
            3. Both left++ and right--
```
We will never  have more than $O(n)$ iterations for the while loop because the pointers start $n$ away from each other and move at least once step closer in every iteration.
### Example 1: Check if a string is palindrome
Given a string `s`, return `true` if it is a palindrome, `false` otherwise.
A string is a palindrome if it reads the same forward as backward. That means, after reversing it, it is still the same string. For example: "abcdcba", or "racecar".
```cpp
bool checkIfPalindrome(string s) {
    int left = 0;
    int right = s.size() - 1;
    
    while (left < right) {
        if (s[left] != s[right]) {
            return false;
        }
        left++;
        right--;
    }
    
    return true;
}
```
This algorithm uses $O(1)$ space and has a time complexity of $O(n)$.
### Example 2: Pair of numbers that sum to target
Given a **sorted** array of unique integers and a target integer, return `true` if there exists a pair of numbers that sum to target, `false` otherwise. This problem is similar to [Two Sum](https://leetcode.com/problems/two-sum/). (In Two Sum, the input is not sorted).

For example, given `nums = [1, 2, 4, 6, 8, 9, 14, 15]` and `target = 13`, return true because `4 + 9 = 13`.
```cpp
bool checkForTarget(vector<int>& nums, int target) {
    int left = 0;
    int right = nums.size() - 1;
    while (left < right) {
        // curr is the current sum
        int curr = nums[left] + nums[right];
        if (curr == target) {
            return true;
        }
        if (curr > target) {
            right--;
        } else {
            left++;
        }
    }

    return false;
}
```
This algorithm uses $O(1)$ space and has a time complexity of $O(n)$.
## Approach 2: Start from the beginning and move simultaneously
This method is only applicable when the problem has two iterables in the input (e.g., two arrays).
```cpp
function fn(arr1, arr2):
    i = j = 0
    while i < arr1.length AND j < arr2.length:
        Do some logic here depending on the problem
        Do some more logic here to decide on one of the following:
            1. i++
            2. j++
            3. Both i++ and j++

    // Step 4: make sure both iterables are exhausted
    // Note that only one of these loops would run
    while i < arr1.length:
        Do some logic here depending on the problem
        i++

    while j < arr2.length:
        Do some logic here depending on the problem
        j++
```
This has a linear time complexity of $O(n + m)$ if the work inside the while loop is $O(1)$, where `n = arr1.length` and `m = arr2.length`. This is because at every iteration, we move at least one pointer forward, and the pointers cannot be moved forward more than n + m times without the arrays being exhausted.
### Example 1: Return the sorted combination of two sorted arrays
Given two sorted integer arrays `arr1` and `arr2`, return a new array that combines both of them and is also sorted.
```cpp
vector<int> combine(vector<int>& arr1, vector<int>& arr2) {
    // ans is the answer
    vector<int> ans;
    int i = 0, j = 0;
    while (i < arr1.size() && j < arr2.size()) {
        if (arr1[i] < arr2[j]) {
            ans.push_back(arr1[i]);
            i++;
        } else {
            ans.push_back(arr2[j]);
            j++;
        }
    }
    
    while (i < arr1.size()) {
        ans.push_back(arr1[i]);
        i++;
    }
    
    while (j < arr2.size()) {
        ans.push_back(arr2[j]);
        j++;
    }
    
    return ans;
}
```
### Example 2: Check if string is a subsequence of another
[Leetcode - is subsequence](https://leetcode.com/problems/is-subsequence/)
Given two strings `s` and `t`, return `true` if `s` is a subsequence of `t`, or `false` otherwise.
A subsequence of a string is a sequence of characters that can be obtained by deleting some (or none) of the characters from the original string, while maintaining the relative order of the remaining characters. For example, "ace" is a subsequence of "abcde" while "aec" is not.
```cpp
class Solution {
public:
    bool isSubsequence(string s, string t) {
        int i = 0, j = 0;
        while (i < s.size() && j < t.size()) {
            if (s[i] == t[j]) {
                i++;
            }
            j++;
        }
        
        return i == s.size();
    }
};
```
This solution uses $O(1)$ space and has a time complexity of $O(length(s) + length(t))$.