# 🧩 LeetCode - Range Sum Query - Immutable

**Link:** [Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/)  
**Difficulty:** Easy  
**Language:** C++  
**Date Solved:** 25/04/2025

---

## 🧠 Problem Description

You're given an integer array `nums`. Your task is to efficiently answer multiple queries of the following type:

> Calculate the sum of elements in the subarray from index `left` to `right`, inclusive.

Implement the `NumArray` class:

- `NumArray(vector<int>& nums)` — Initializes the object with the array `nums`.
- `int sumRange(int left, int right)` — Returns the sum of the subarray from `nums[left]` to `nums[right]`, inclusive.

---

## 💡 Approach

To answer multiple range sum queries efficiently, we use a **prefix sum array**.

This array stores cumulative sums such that `prefix[i] = nums[0] + nums[1] + ... + nums[i]`.  
With this structure, we can compute any range sum `sumRange(left, right)` in **constant time** using:

```cpp
prefix[right] - prefix[left - 1]  // if left > 0
prefix[right]                    // if left == 0
```
---

## 🔍 Complexity

- **Time:** O(n) for the constructor and O(1) for the function sumRange (due to prefix sum Array)
- **Space:** O(n) as we have to create a new array for the sum prefix

---

## 🧪 Code

```cpp
class NumArray {
vector<int> prefixSum;
public:
    NumArray(vector<int>& nums) {
        prefixSum.resize(nums.size());
        prefixSum[0] = nums[0];
        for(int i = 1; i < nums.size(); i++) {
            prefixSum[i] = nums.at(i) + prefixSum[i - 1];
        }
    }
    
    int sumRange(int left, int right) {
        return left > 0 ? prefixSum[right] - prefixSum[left - 1] : prefixSum[right];
    }
};

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray* obj = new NumArray(nums);
 * int param_1 = obj->sumRange(left,right);
 */
