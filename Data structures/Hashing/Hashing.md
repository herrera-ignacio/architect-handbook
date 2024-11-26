# Hashing
## Definition
Use of hash function to index a [[Hash map]] is called *hashing* or *scatter-storage addressing*.
Hashing is a computationally- and storage-space-efficient form of data access that **avoids the non-constant access time** of ordered and unordered lists and structured trees, and the often-exponential storage requirements of direct access of state spaces of large or variable-length keys.
## Examples
### Example: Group anagrams
Given an array of strings `strs`, group the [anagrams](https://en.wikipedia.org/wiki/Anagram) together.
For example, given `strs = ["eat","tea","tan","ate","nat","bat"]`, return `[["bat"],["nat","tan"],["ate","eat","tea"]]`.

--- 
We can use two hash maps to check if two strings ara anagrams of each other: count all the characters in each string, then compare if the hash maps are the same. However, this is very cumbersome to implement. The cleanest way is by **checking if they are equal after both being sorted**. 
Then, we can use the sorted version as a key in a hash map and map these keys to the group themselves.
Essentially, every group has its own identifier (i.e., the sorted string).
```js
/**
 * @param {string[]} strs
 * @return {string[][]}
 */
var groupAnagrams = function(strs) {
    let groups = new Map();
    for (const s of strs) {
        let key = s.split('').sort().join('');
        if (!groups.has(key)) {
            groups.set(key, []);
        }
        
        groups.get(key).push(s);
    }

    let ans = [];
    for (const group of groups.values()) {
        ans.push(group);
    }
    
    return ans;
};
```

```python
from collections import defaultdict

class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        groups = defaultdict(list)
        for s in strs:
            key = "".join(sorted(s))
            groups[key].append(s)
        
        return groups.values()
```
Given $n$ as the length of `strs` and $m$ as the average length of the strings, we iterate over each string and sort it, which costs $O(n \cdot m \cdot \log m)$. Then, we iterate over the keys. In the worst case scenario, when there are no matching anagrams, there will be $n$ groups, which means this will cost $O(n)$, giving an overall time complexity of $O(n \cdot m \cdot \log m)$ (the final $+n$ is dominated).
The space complexity is $O(n \cdot m)$ as each string will be placed in an array within the hash map.

> [!tip] Alternative solution
> Another way to solve this problem is to use a tuple of length 26 representing the count of each character as the key instead of the sorted string. This would technically solve the problem in $O(n \cdot m)$ because the 26 is a constant defined by the problem, but fo the test cases with smaller strings it would be slower due to the constant factor which is hidden by big O. It also assumes that the strings can only have 26 different characters.
### Example: Minimum consecutive cards to pick up
Given an integer array `cards`, find the length of the shortest subarray that contains at least one duplicate. If the array has no duplicates, return `-1`.

--- 
This question is equivalent to what is the shortest distance between any two of the same element? If we go through the array and use a hash map to record the indices for every element, we can iterate over those indices to find the shortest distance.
 For example, given `cards = [1, 2, 6, 2, 1]`, we would map `1: [0, 4]`, `2: [1, 3]`, and `6: [2]`.
 Then we can iterate over the values and see that the minimum difference can be achieved from picking up the `2`s.
 ```js
 /**
 * @param {number[]} cards
 * @return {number}
 */
var minimumCardPickup = function(cards) {
    let dic = new Map();
    for (let i = 0; i < cards.length; i++) {
        if (!dic.has(cards[i])) {
            dic.set(cards[i], []);
        }
        dic.get(cards[i]).push(i);
    }
    
    let ans = Infinity;
    for (const [key, arr] of dic) {
        for (let i = 0; i < arr.length - 1; i++) {
            ans = Math.min(ans, arr[i + 1] - arr[i] + 1);
        }
    }
    
    return ans == Infinity ? -1 : ans;
};
```

```python
from collections import defaultdict

class Solution:
    def minimumCardPickup(self, cards: List[int]) -> int:
        dic = defaultdict(list)
        for i in range(len(cards)):
            dic[cards[i]].append(i)
            
        ans = float("inf")
        for key in dic:
            arr = dic[key]
            for i in range(len(arr) - 1):
                ans = min(ans, arr[i + 1] - arr[i] + 1)
        
        return ans if ans < float("inf") else -1
```
The time complexity is still $O(n)$ because the inner loop in the nested loop can only iterate $n$ times in total, since it's iterating over indices of elements from the array.
We can actually improve this algorithm slightly by observing that we don't need to store all the indices, but only the most recent one that we saw for each number. This improves the average space complexity, being $O(n)$ only in the worst case.
```js
/**
 * @param {number[]} cards
 * @return {number}
 */
var minimumCardPickup = function(cards) {
    let dic = new Map();
    let ans = Infinity;
    for (let i = 0; i < cards.length; i++) {
        if (dic.has(cards[i])) {
            ans = Math.min(ans, i - dic.get(cards[i]) + 1);
        }
        
        dic.set(cards[i], i);
    }

    return ans == Infinity ? -1 : ans;
};
```
### Max sum of a pair with equal sum of digits
Given an array of integers `nums`, find the maximum value of `nums[i] + nums[j]`, where `nums[i]` and `nums[j]` have the same **digit sum** (the sum of their individual digits). Return `-1` if there is no pair of numbers with the same digit sum.

---
We iterate through the array and group all the numbers with the same digit sum in a hash map. Then we can iterate over that hash map and for each group with at least 2 elements, find the 2 max elements by sorting.
```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maximumSum = function(nums) {
    let getDigitSum = num => {
        let digitSum = 0;
        while (num > 0) {
            digitSum += num % 10;
            num = Math.floor(num / 10);
        }
        
        return digitSum;
    }
    
    let dic = new Map();
    for (const num of nums) {
        let digitSum = getDigitSum(num);
        if (!dic.has(digitSum)) {
            dic.set(digitSum, []);
        }
        dic.get(digitSum).push(num);
    }
    
    let ans = -1;
    for (const [key, curr] of dic) {
        if (curr.length > 1) {
            curr.sort((a, b) => b - a);
            ans = Math.max(ans, curr[0] + curr[1]);
        }
    }
    
    return ans;
};
```

This algorithm is inefficient due to the sorting, which can potentially cost $O(n \cdot n)$ if every number in the input has the same digit sum, where $n$ is the length of the input array.
However, we don't need to store all the numbers in the group. Instead, we just save the largest number seen so far for each digit sum.
```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maximumSum = function(nums) {
    let getDigitSum = num => {
        let digitSum = 0;
        while (num > 0) {
            digitSum += num % 10;
            num = Math.floor(num / 10);
        }
        
        return digitSum;
    }
    
    let dic = new Map();
    let ans = -1;
    for (const num of nums) {
        let digitSum = getDigitSum(num);
        if (dic.has(digitSum)) {
            ans = Math.max(ans, num + dic.get(digitSum));
        }
        
        dic.set(digitSum, Math.max(dic.get(digitSum) || 0, num));
    }
    
    
    return ans;
};
```
This give us a time complexity of $O(n)$ and the same space complexity because in the worst case we store all the elements in hash map's values, but with the improvement, the average case will use much less space since each key only stores an integer.
### Example: Equal row and column pairs
Given an `n x n` matrix `grid`, return the number of pairs `(R, C)` where `R` is a row and `C` is a column, and `R` and `C` are equal if we consider them as 1D arrays.
For example, let's say there are three rows that look like `[1, 2, 3]`, and there are two columns that look the same. For each of the three rows, there are two columns to pair with, so that means there are `3 * 2 = 6` pairs.

---
We can use a hash map to count how many times each row occurs. We can use a second hash map to do the same thing with the columns.
Then, we can iterate over the rows hash map, and for each row, check if the same array appeared as a column. If it did, then the product of the number of appearances is added to our answer.
The problem is, arrays can't be put in a hash map as a key because they are mutable. We need to convert the rows and columns into a "hashable" form such as a string or tuple. The best choice will depend on the language you're using.

```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var equalPairs = function(grid) {
    let convertToKey = arr => {
        let key = "";
        for (const num of arr) {
            key += num + ",";
        }
	        
        return key;
    }
    
    let dic = new Map();
    for (const arr of grid) {
        let key = convertToKey(arr);
        dic.set(key, (dic.get(key) || 0) + 1);
    }
    
    let dic2 = new Map();
    for (let col = 0; col < grid[0].length; col++) {
        let currentCol = [];
        for (let row = 0; row < grid.length; row++) {
            currentCol.push(grid[row][col]);
        }
        
        let key = convertToKey(currentCol);
        dic2.set(key, (dic2.get(key) || 0) + 1);
    }
    
    let ans = 0;
    for (const [key, val] of dic) {
        ans += val * dic2.get(key) || 0;
    }
    
    return ans;
};
```

```python
from collections import defaultdict

class Solution:
    def equalPairs(self, grid: List[List[int]]) -> int:
        def convert_to_key(arr):
            # Python is quite a nice language for coding interviews!
            return tuple(arr)
        
        dic = defaultdict(int)
        for row in grid:
            dic[convert_to_key(row)] += 1
        
        dic2 = defaultdict(int)
        for col in range(len(grid[0])):
            current_col = []
            for row in range(len(grid)):
                current_col.append(grid[row][col])
            
            dic2[convert_to_key(current_col)] += 1

        ans = 0
        for arr in dic:
            ans += dic[arr] * dic2[arr]
        
        return ans
```
If the grid has a size of $n \cdot n$ , this algorithm has a time complexity of $O(n^2)$ - there are $n^2$ elements and each element is iterated over twice initially (once for the row it occupies and once for the column it occupies). Populating and iterating over the hash maps will be dominated by this.
The space complexity is also $O(n^2)$ because if all rows and columns are unique, then each of the two hash maps will both grow to a size of $n$, with each key having a length of $n$.