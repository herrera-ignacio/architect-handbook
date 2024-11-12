# Prefix sum
## Overview
Prefix sum is a technique that can be used on array (of numbers). The idea is to create an array `prefix` where `prefix[i]` is the sum of all elements up to the index `i` (inclusive).
For example, given `nums = [5,2,1,6,3,8]`, we would have `prefix = [5,7,8,14,17,25]`.
It allows us to find the sum of any subarray in $O(1)$. If we want the sum of the subarray from `i` to `j` (inclusive), then the answer is `prefix[j] - prefix[i - 1]`, or `prefix[j] - prefix[i] + nums[i]` if you don't want to deal with the out of bounds case when `i = 0`.
![[Pasted image 20241112114017.png]]
## Pseudocode
```
Given an array nums,

prefix = [nums[0]]
for (int i = 1; i < nums.length; i++)
    prefix.append(nums[i] + prefix[prefix.length - 1])
```
- Start with just the first element.
- Iterate with `i` starting from index `1`.
- At any given point, the last element of `prefix` will represent the sum of all the elements in the input `nums` up to but not including the index `i`.
- We add the value from `nums[i]` to the end of `prefix` and continue to the next element.
## When to use it
Whenever a **problem involves sums of a subarray**. It only costs $O(n)$ to build but allows all future subarray queries to be $O(1)$.

> [!info] Pre-processing
> Building a prefix sum is a form of **pre-processing**, we store pre-computed data in a data structure before running the main logic of our algorithm. It's an investment that will save us a huge amount of time during the main parts of the algorithm.
## Examples
### Return if the sum of the array from x to y is less than limit
Given an integer array `nums`, an array `queries` where `queries[i] = [x, y]` and an integer `limit`, return a boolean array that represents the answer to each query. A query is `true` if the sum of the subarray from `x` to `y` is less than `limit`, or `false` otherwise.
For example, given `nums = [1, 6, 3, 2, 7, 2]`, `queries = [[0, 3], [2, 5], [2, 4]]`, and `limit = 13`, the answer is `[true, false, true]`. For each query, the subarray sums are `[12, 14, 12]`.
Let's build a prefix sum and then use the method described above to answer each query in $O(1)$.
```js
/**
 * @param {number[]} nums
 * @param {number[][]} queries
 * @param {number} limit
 * @return {boolean[]}
 */
var answerQueries = function(nums, queries, limit) {
    let prefix = [nums[0]];
    for (let i = 1; i < nums.length; i++) {
        prefix.push(nums[i] + prefix[prefix.length - 1]);
    }
    
    let ans = [];
    for (const [x, y] of queries) {
        let curr = prefix[y] - prefix[x] + nums[x];
        ans.push(curr < limit);
    }
    
    return ans;
};
```
Without the prefix sum, answering each query would be $O(n)$ in the worst case, where $n$ is the length of `nums`. If `m = queries.length`, that would give a time complexity of $O(n*m)$ .
With the prefix sum, it costs $O(n)$ to build, but then answering each query is $O(1)$ which is much better.
### Number of ways to split array
Given an integer array `nums`, find the number of ways to split the array into two parts so that the first section has a sum greater than or equal to the sum of the second section. The second section should have at least one number.
If we build a prefix sum first, we iterate over each index and we can calculate the sums of the left and right sections in $O(1)$, which would improve the time complexity to $O(n)$.
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var waysToSplitArray = function(nums) {
    let n = nums.length;
    
    let prefix = [nums[0]];
    for (let i = 1; i < n; i++) {
        prefix.push(nums[i] + prefix[prefix.length - 1]);
    }
    
    let ans = 0;
    for (let i = 0; i < n - 1; i++) {
        let leftSection = prefix[i];
        let rightSection = prefix[n - 1] - prefix[i];
        if (leftSection >= rightSection) {
            ans++;
        }
    }
    
    return ans;
};
```
Alternatively, you can calculate `leftSection` on the fly and pre-compute the sum of the entire input as `total`, then calculate `rightSection` as `total - leftSection`.
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var waysToSplitArray = function(nums) {
    let ans = 0, leftSection = 0, total = 0;
    for (const num of nums) {
        total += num;
    }
    
    for (let i = 0; i < nums.length - 1; i++) {
        leftSection += nums[i];
        let rightSection = total - leftSection;
        if (leftSection >= rightSection) {
            ans++;
        }
    }
    
    return ans;
};
```
We have improved the space complexity to $O(1)$, which is a great improvement.
