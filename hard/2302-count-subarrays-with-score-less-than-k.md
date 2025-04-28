# 🧩 LeetCode - Count Subarrays With Score Less Than K

**Link:** [Count Subarrays With Score Less Than K](https://leetcode.com/problems/count-subarrays-with-score-less-than-k/)  
**Difficulty:** Hard  
**Language:** C++  
**Date Solved:** 28/04/2025

---

## 🧠 Problem Description

The score of an array is defined as the product of its sum and its length.

    For example, the score of [1, 2, 3, 4, 5] is (1 + 2 + 3 + 4 + 5) * 5 = 75.

Given a positive integer array nums and an integer k, return the number of non-empty subarrays of nums whose score is strictly less than k.

A subarray is a contiguous sequence of elements within an array.

---

## 💡 Approach

We can solve this problem using a two-pointer technique.

We maintain a window [left, right] and keep track of the sum of its elements.
The result is computed as:
```
result = sum * (right - left + 1)
```
Whenever the result is greater than or equal to k, we move left to shrink the window.

Once the window satisfies score < k, all subarrays that end at right and start between left and right are valid.
Thus, we can count them by:
```
count += right - left + 1
```
---

## 🔍 Complexity

- **Time:** O(n) for the constructor and O(1) for the function sumRange (due to prefix sum Array)
- **Space:** O(n) as we have to create a new array for the sum prefix

---

## 🧪 Code

```cpp
class Solution {
public:
    long long countSubarrays(vector<int>& nums, long long k) {
         if (k <= 1) return 0;
        long long result = 0, sum = 0, right = 0, left = 0, totalCount = 0;
        while(nums.size() > right) {
            sum += nums[right];
            result = sum * (right - left + 1);
            while(result >= k) {
                sum -= nums[left++];
                result = sum * (right - left + 1);
            }
            totalCount += right - left + 1;
            right++;
        }

        return totalCount;
    }
};