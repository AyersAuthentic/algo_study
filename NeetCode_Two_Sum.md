## 📝 LeetCode 1: Two Sum

  * **Date Solved:** September 30, 2025
  * **Link:** [Two Sum](https://leetcode.com/problems/two-sum/)

-----

### \#\# 🎯 Problem Summary

Given an array of integers `nums` and a target integer `target`, the goal is to find the indices of the two numbers in the array that add up to the target. It is guaranteed that each input has exactly one solution, and you may not use the same element twice.

-----

### \#\# 🧠 Key Concepts Tested

This is arguably the most famous coding interview question. It's a fundamental test of your understanding of hash maps and time complexity.

  * **Hash Maps (Dictionaries):** The optimal solution relies on the $O(1)$ average time complexity of hash map lookups to avoid a brute-force search.
  * **Time/Space Complexity Trade-off:** The problem highlights the classic strategy of using extra memory (a hash map) to significantly improve the runtime of a solution.
  * **"Complement" Lookups:** The core pattern involves calculating a "complement" (`target - current_number`) and then efficiently checking if that complement has been seen before.

-----

### \#\# ✅ Solution Approaches

#### \#\#\# Approach 1: Brute Force (Nested Loops)

The most intuitive solution is to check every possible pair of numbers.

```python
class Solution:
    def twoSum_brute_force(self, nums: List[int], target: int) -> List[int]:
        n = len(nums)
        for i in range(n):
            for j in range(i + 1, n):
                if nums[i] + nums[j] == target:
                    return [i, j]
```

  * **Time Complexity: $O(n^2)$** - The nested loops lead to a quadratic runtime, which is too slow for large inputs.
  * **Space Complexity: $O(1)$** - No extra space is used that scales with the input size.

#### \#\#\# Approach 2: One-Pass Hash Map (Optimal Solution)

This is the standard, most efficient solution expected in interviews. The key insight is to build the hash map and check for the complement in the same loop.

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # Hash map to store the number and its index: {val -> index}
        indices = {}

        # Iterate through the list with both index and value
        for i, n in enumerate(nums):
            # Calculate the complement we are looking for
            diff = target - n
            
            # First, check if the complement exists in our map
            if diff in indices:
                # If it does, we have found our pair
                return [indices[diff], i]
            
            # If not, add the current number and its index to the map
            # for future lookups.
            indices[n] = i
```

  * **Logic:** For each number, we check if its complement has been seen *before*. If it has, we've found our solution. If not, we add the current number to our map of "seen" numbers so that future elements can use it as a complement.
  * **Time Complexity: $O(n)$** - We iterate through the array of *n* numbers only once. Each hash map lookup and insertion is, on average, a constant time operation.
  * **Space Complexity: $O(n)$** - In the worst-case scenario, we store all *n* elements in the hash map.

-----

### \#\# 💡 Key Takeaways & Interview Prep Notes

1.  **This is the Canonical Hash Map Problem:** If an interviewer asks this question, they are testing one thing: "Do you know how to use a hash map to optimize a search?" Your first thought should be to trade space for time.

2.  **The One-Pass Method is Key:** While a two-pass hash map solution works, the one-pass approach is more elegant and efficient. It cleverly solves the problem of not using the same element twice by only adding an element to the map *after* checking for its complement.

3.  **Verbalize the Logic:** In an interview, walk through the one-pass solution with an example. Explain *why* it works: "The hash map stores numbers we've already passed. By the time we get to the second number of the pair, its complement will already be in the map, and we can immediately return the answer." This demonstrates a deep understanding.
