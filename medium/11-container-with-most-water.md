# 🔢 Container With Most Water

**Link:** [https://leetcode.com/problems/container-with-most-water/](https://leetcode.com/problems/count-complete-subarrays-in-an-array/)

**Difficulty:** Medium  
**Date:** 28/04/2025  
**Language:** C++

---

## 🧠 Problem Description

You are given an integer array ```height``` of length ```n```. There are ```n``` vertical lines drawn such that the two endpoints of the ```i^th``` line are ```(i, 0)``` and ```(i, height[i])```.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

---

## 💡 Approach

We use the two pointers technique, initializing one pointer at the beginning (left = 0) and the other at the end (right = height.size() - 1) of the array.

At each step:

    We calculate the area formed by the two lines, using the formula:
    Area=min(height[left], height[right])×(right−left)
    Area=min(height[left], height[right])×(right−left)

    We update the maximum area found so far.

After calculating the area:

We move the pointer corresponding to the smaller height, because the area is limited by the shorter line.

Moving the taller line wouldn't help, since reducing the width without increasing the minimum height would only decrease the area.

We continue this process until the two pointers meet

---

## 🔍 Complexity

- **Time:** O(n) As we use the two pointers strategy
- **Space:** O(1) As the variables does not depends on the array

---

## 🧪 Code

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int right = height.size() - 1;
        int maxArea = 0, minHeight = 0, left = 0;
        while(right > left) {
            minHeight = min(height[left], height[right]);
            maxArea = max(maxArea, minHeight * (right - left));
            if(height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }
        return maxArea;
    }
};