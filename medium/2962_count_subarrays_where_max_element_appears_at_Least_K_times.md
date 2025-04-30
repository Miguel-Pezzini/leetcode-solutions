# 🔢 Count Subarrays Where Max Element Appears at Least K Times

**Link:** [https://leetcode.com/problems/count-subarrays-where-max-element-appears-at-least-k-times/](https://leetcode.com/problems/count-subarrays-where-max-element-appears-at-least-k-times/)

**Difficulty:** Medium  
**Date:** 30/04/2025  
**Language:** C++
---

## 🧠 Problem Description

You are given an integer array ```nums``` and a positive integer ```k```.

Return the number of subarrays where the maximum element of ```nums``` appears at least ```k``` times in that subarray.

A subarray is a contiguous sequence of elements within an array.

---

## 💡 Approach

1. ### Find the maximum element in the array (max)
The algorithm starts by iterating through the array nums to determine the maximum value present. This value will be used as a reference throughout the rest of the process.

2. ### Apply the sliding window technique
A two-pointer approach is used with variables start and ```i``` to define a dynamic window over the array.

Every time we encounter the maximum element ```max```, we increment a counter called ```maxElementsInWindow```.

Once this counter reaches exactly ```k```, it means we have a subarray where the maximum element appears ```k``` times.

To maintain the window condition (i.e., having less than k max elements), we increment the start pointer and decrease the counter when we remove a max from the window.

At each step, we add start to the result ```ans```. This works because there are exactly start subarrays ending at index ```i``` that do not satisfy the condition, so all the others do.

---

## 🔍 Complexity

- **Time:** O(n) As we use just one loop and the while is linear
- **Space:** O(1) As the variables does not depends on the array

---

## 🧪 Code

```cpp
class Solution {
public:
    long long countSubarrays(vector<int>& nums, int k) {
        long long  max = 0, start = 0, ans = 0;
        for(int i = 0; i < nums.size(); i++) {
            if(nums.at(i) > max) {
                max = nums.at(i);
            }
        }
        int maxElementsInWindow = 0;
        for(int i = 0; i < nums.size() ;i++) {
            if(nums.at(i) == max) {
                maxElementsInWindow++;
            }
            while(maxElementsInWindow == k) {
                if(nums[start] == max) {
                    maxElementsInWindow--;
                }
                start++;
            }
            ans += start;
        }
        return ans;
    }
};