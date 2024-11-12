# Sliding window
## Overview
Sliding window solves a common group of problems involving subarrays and is implemented using [[Two pointers]].
The idea behind a sliding window is to consider only valid subarrays (defined by left and right bounds). In sliding window, we maintain two variables `left` and `right`, which at any given time represent the current subarray under consideration.

> [!tip] Applies to string too
> Like two pointers, sliding windows work the same with arrays and strings - the important thing is that they're iterables with ordered elements.
## Pseudocode
Initially, we have `left = right = 0`, which means that the first subarray we look at is just the first element of the array on its own. We want to expand the size of our "window", and we do that by incrementing `right`. When we increment right, this is like "*adding*" a new element to our window.
```
function fn(arr):
    left = 0
    for (int right = 0; right < arr.length; right++):
        Do some logic to "add" element at arr[right] to window

        while WINDOW_IS_INVALID:
            Do some logic to "remove" element at arr[left] from window
            left++

        Do some logic to update the answer
```
But what if after adding a new element, the subarray becomes invalid? We need to "*remove*" some elements from our window until it becomes valid again. To "remove" elements, we can increment left, which shrinks our window.
As we add and remove elements, we are "**sliding**" our window along the input from left to right, until we reach the end of the input.
![[Pasted image 20241111194533.png]]
## When should we use sliding window?

### Subarrays/substrings
> [!info]
> As a reminder, a subarray or substring is a contiguous section of an array or string.
Think about sliding windows if a problem has explicit constraints such as:
- Sum greater than or less than `k`.
- Limits on what is contained, such as the maximum of `k` unique elements or no duplicates allowed.
And/or asks for:
- Minimum or maximum length
- Number of subarrays/substrings
### Generalization
**First**, the problem will either explicitly or implicitly **define criteria that make a subarray "valid"**. There are 2 components regarding what makes a subarray valid:
1. **A constraint metric**. This is some attribute of a subarray. It could be the sum, the number of unique elements, the frequency of a specific element, or any other attribute.
2. **A numeric restriction on the constraint metric.** This is what the constraint metric should be for a subarray to be considered valid.
Second, the problem will ask you to **find valid subarrays** in some way.
1. The most common task you will see is finding the **best** valid subarray. The problem will define what makes a subarray **better** than another. For example, a problem might ask you to find the **longest** valid subarray.
2. Another common task is finding the number of valid subarrays.
Some common problem descriptions would be:
- Find the longest subarray with a sum less than or equal to `k`.
- Find the longest substring that has at most one `"0"`.
- Find the number of subarrays that have a product less than `k`.
## Fixed window size
Sometimes, a problem will specify a fixed length k. This usually simplifies the problems because the difference between any two adjacent windows is only two elements (we add one element on the right and remove one on the left to maintain the length).
Start by building the first window (from index 0 to k - 1). Once we have a window of size k, if we add an element at index i, we need to remove the element at index i - k. For example, k = 2 and you currently have elements at indices `[0, 1]`. Now, we add 2: `[0, 1, 2]`. To keep the window size at k = 2, we need to remove` 2 - k = 0`: `[1, 2]`.
```
function fn(arr, k):
    curr = some data to track the window

    // build the first window
    for (int i = 0; i < k; i++)
        Do something with curr or other variables to build first window

    ans = answer variable, probably equal to curr here depending on the problem
    for (int i = k; i < arr.length; i++)
        Add arr[i] to window
        Remove arr[i - k] from window
        Update ans

    return ans

```
## Why is sliding window efficient?
For any array, there are $n-1$ subarrays of length 2 (every index except the last one can be a starting index), $n-2$ subarrays of length 3, and so on until there is only 1 subarray of length $n$.  This means there are $\sum_{k=1}^{n} k = \frac{n \cdot (n+1)}{2}$ subarrays. 
In terms of time complexity, any algorithm that looks at every subarray will be at least $O(n^2)$, which is usually too slow. **A sliding window guarantees a maximum of $2n$ window iterations** — the right pointer can move $n$ times and the left pointer can move $n$ times. This means that if logic done for each window is $O(1)$, **sliding window algorithms run in $O(n)$** which is much faster.

> [!tip] Amortized analysis of the nested loop
> Even though there’s a nested loop (to remove values from the sliding window), the while loop can only iterate n times in total for the entire algorithm because left starts at 0, only increases, and never exceeds n. This is what we refer to as [amortized analysis](https://en.wikipedia.org/wiki/Amortized_analysis) — even though the worst case for an iteration inside the for loop is O(n) it averages out to O(1) when you consider the entire runtime of the algorithm.
## Examples: find the best valid subarray
### Find the longest subarray whose sum is less than or equal to k
Given an array of positive integers `nums` and an integer k, find the length of the longest subarray whose sum is less than or equal to k.
```cpp
int findLength(vector<int>& nums, int k) {
    // curr is the current sum of the window
    int left = 0, curr = 0, ans = 0;
    for (int right = 0; right < nums.size(); right++) {
        curr += nums[right];
        while (curr > k) {
            curr -= nums[left];
            left++;
        }
        
        ans = max(ans, right - left + 1);
    }
    
    return ans;
}
```
This algorithm has a time complexity of $O(n)$ since all the work done inside the for loop is amortized $O(1)$.
### Find the longest substring achievable that contains only "1"s
You are given a binary string s (a string containing only "0" and "1"). You may choose up to one "0" and flip it to a "1". What is the length of the longest substring achievable that contains only "1"?
For example, given s = "1101100111", the answer is 5. If you perform the flip at index 2, the string becomes "1111100111".
> [!tip]
> Because the string can only contain "1" and "0", another way to look at this problem is "what is the longest substring that contains at most one "0"?
```cpp
int findLength(string s) {
    // curr is the current number of zeros in the window
    int left = 0, curr = 0, ans = 0;
    for (int right = 0; right < s.size(); right++) {
        if (s[right] == '0') {
            curr++;
        }
        
        while (curr > 1) {
            if (s[left] == '0') {
                curr--;
            }
            left++;
        }
        
        ans = max(ans, right - left + 1);
    }
    
    return ans;
}
```
This algorithm has a time complexity of $O(n)$ since all the work done inside the for loop is amortized $O(1)$.
## Examples: find the number of valid subarrays
If a problem asks for **the number of subarrays that fit some constraint**, we can still use sliding window, but we need to use a neat **math trick** to calculate the number of subarrays.
Let's say that we are using the sliding window algorithm we have learned and currently have a window `(left, right)`. How many valid windows end at index right? There's the current window `(left, right)`, then `(left + 1, right)`, `(left + 2, right)`, and so on until `(right, right)` (only the element at right). Therefore, the number of valid windows ending at index `right` is equal to the size of the window, which we know is `right - left + 1`.
### Number of subarrays where the product of elements is less than `k`
> [LeetCode - Subarray product less than k](https://leetcode.com/problems/subarray-product-less-than-k/)

Given an array of positive integers `nums` and an integer `k`, return the number of subarrays where the product of all the elements in the subarray is strictly less than `k`.
For example, given the input `nums = [10, 5, 2, 6]`, `k = 100`, the answer is 8. The subarrays with products less than k are: `[10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6]`.
```cpp
class Solution {
public:
    int numSubarrayProductLessThanK(vector<int>& nums, int k) {
        if (k <= 1) {
            return 0;
        }

        int ans = 0, left = 0, curr = 1;
        for (int right = 0; right < nums.size(); right++) {
            curr *= nums[right];
            while (curr >= k) {
                curr /= nums[left];
                left++;
            }
            
            ans += right - left + 1;
        }
        
        return ans;
    }
};
```
## Examples: fixed window size
### Find the sum of the subarray with the largest sum whose length is `k`
Given an integer array `nums` and an integer `k`, find the sum of the subarray with the largest sum whose length is `k`.
```cpp
int findBestSubarray(vector<int>& nums, int k) {
    int curr = 0;
    for (int i = 0; i < k; i++) {
        curr += nums[i];
    }
    
    int ans = curr;
    for (int i = k; i < nums.size(); i++) {
        curr += nums[i] - nums[i - k];
        ans = max(ans, curr);
    }
    
    return ans;
}
```