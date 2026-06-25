# LeetCode 11 - Container With Most Water

## Problem

You are given an integer array `height` where each element represents the height of a vertical line drawn on the x-axis.

Choose two lines such that together with the x-axis they form a container that holds the **maximum amount of water**.

Return the maximum amount of water the container can store.

---

## Example

```python id="33occm"
height = [1,8,6,2,5,4,8,3,7]
```

Output:

```python id="zj7wqf"
49
```

---

## Pattern Used

* **Two Pointers**
* **Greedy Pointer Movement**

---

## Intuition

To form a container using two lines:

* The **width** is the distance between the two pointers:

  ```python id="q0skl0"
  right - left
  ```
* The **height** of water is limited by the smaller of the two heights:

  ```python id="3hlhbn"
  min(height[left], height[right])
  ```

So the water stored is:

```python id="89k36w"
(right - left) * min(height[left], height[right])
```

The key idea is:

* Start with the **widest possible container** using the leftmost and rightmost lines.
* Calculate the area.
* Move the pointer pointing to the **smaller height**, because the smaller line is the bottleneck limiting the area.

---

## Approach

1. Initialize two pointers:

   * `left = 0`
   * `right = len(height) - 1`
2. While `left < right`:

   * Compute the width.
   * Compute the minimum height.
   * Compute the current area.
   * Update the maximum area found so far.
3. Move the pointer with the **smaller height**:

   * If `height[left] < height[right]`, move `left`
   * Otherwise, move `right`
4. Return the maximum area.

---

## Python Solution

```python id="83opwa"
from typing import List

class Solution:
    def maxArea(self, height: List[int]) -> int:
        left = 0
        right = len(height) - 1
        max_area = 0

        while left < right:
            width = right - left
            curr_height = min(height[left], height[right])
            area = width * curr_height

            max_area = max(max_area, area)

            if height[left] < height[right]:
                left += 1
            else:
                right -= 1

        return max_area
```

---

## Time Complexity

* **O(n)**
  Because each pointer moves inward at most once across the array.

## Space Complexity

* **O(1)**
  Only a few extra variables are used.

---

## What I Learned

* How to use **Two Pointers** to optimize a brute-force problem.
* Why the area depends on both **width** and the **minimum height**.
* Why moving the pointer at the smaller height is the correct greedy choice.
* How to keep track of the best answer while scanning from both ends.
