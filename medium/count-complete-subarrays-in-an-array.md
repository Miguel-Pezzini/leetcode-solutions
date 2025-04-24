# 🔢 Count Complete Subarrays

**Link:** [https://leetcode.com/problems/count-complete-subarrays-in-an-array/](https://leetcode.com/problems/count-complete-subarrays-in-an-array/)

**Difficulty:** Medium  
**Date:** 24/04/2025  
**Language:** C++

---

## 🧠 Problem Description

- You are given an array `nums` consisting of positive integers.
- A subarray is called **complete** if the number of distinct elements in the subarray is equal to the number of distinct elements in the whole array.
- Return the total number of complete subarrays.

---

## 💡 Approach

We use a `bitset<2001>` to efficiently track which elements are present in the current subarray and in the whole array.

### Steps:
- 1. First, count how many distinct elements exist in the entire array using `bitset`.
- 2. For every subarray starting at `i`, create a new `bitset` and count how many distinct elements appear from `i` to `j`.
- 3. If the current count equals the total, increment the result.

- This approach improves performance significantly over using `set` or `unordered_set`.

---

## 🔍 Complexity

- **Time:** O(n²), due to nested loops over subarrays
- **Space:** O(1) (since `bitset<2001>` uses fixed space)

---

## 🧪 Code

```cpp
class Solution {
public:
    int countCompleteSubarrays(vector<int>& nums) {
        bitset<2001> totalBits;
        int totalDistinct = 0;
        for (int num : nums) {
            if (!totalBits.test(num)) {
                totalBits.set(num);
                totalDistinct++;
            }
        }

        int count = 0;

        for (size_t i = 0; i < nums.size(); i++) {
            bitset<2001> currentBits;
            int currentDistinct = 0;

            for (size_t j = i; j < nums.size(); j++) {
                int num = nums[j];
                if (!currentBits.test(num)) {
                    currentBits.set(num);
                    currentDistinct++;
                }

                if (currentDistinct == totalDistinct) {
                    count++;
                }
            }
        }

        return count;
    }
};
