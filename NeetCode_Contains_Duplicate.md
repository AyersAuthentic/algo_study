## 📝 LeetCode 217: Contains Duplicate

  * **Date Solved:** September 25, 2025
  * **Link:** [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

-----

### \#\# 🎯 Problem Summary

The goal is to determine if an array of integers, `nums`, contains any duplicate values. If any number appears more than once, return `true`; otherwise, return `false`.

-----

### \#\# 🧠 Key Concepts Tested

This is a fundamental "uniqueness" problem that directly tests your understanding of the trade-offs between different data structures.

  * **Hash Sets:** The optimal solution uses a Hash Set for its highly efficient average-case $O(1)$ time complexity for insertions and lookups.
  * **Time Complexity Analysis:** Evaluating how the runtime of an algorithm scales with the size of the input (e.g., $O(n^2)$ vs. $O(n)$).
  * **Space Complexity Analysis:** Evaluating how much additional memory an algorithm requires based on the input size.

-----

### \#\# ✅ Solution Approaches

#### \#\#\# Approach 1: Brute Force (Nested Loops)

The most straightforward, but least efficient, approach is to compare every element with every other element in the array.

```python
def containsDuplicate_brute_force(nums):
    n = len(nums)
    for i in range(n):
        for j in range(i + 1, n):
            if nums[i] == nums[j]:
                return True
    return False
```

  * **Time Complexity: $O(n^2)$** - The nested loops mean that for each of the *n* elements, we are iterating through the rest of the array. This is too slow for large inputs.
  * **Space Complexity: $O(1)$** - We are not using any extra space that scales with the input size.

#### \#\#\# Approach 2: Using a Hash Set (Optimal Solution)

This is the preferred and most efficient solution. We can iterate through the array once, using a hash set to keep track of the numbers we've already seen.

```python
def containsDuplicate_hash_set(nums):
    seen = set()
    for num in nums:
        if num in seen:
            return True
        seen.add(num)
    return False
```

  * **Why it works:** A hash set provides average $O(1)$ time for checking if an element `in seen` and for `seen.add(num)`. By iterating through the array once, we check if the current number is already in our set of "seen" numbers. If it is, we've found a duplicate. If not, we add it to the set and continue.
  * **Time Complexity: $O(n)$** - We iterate through the list of *n* numbers only once. Each hash set operation takes, on average, constant time.
  * **Space Complexity: $O(n)$** - In the worst-case scenario (no duplicates), we would store all *n* elements from the input array in our hash set.

-----

### \#\# 💡 Key Takeaways & Interview Prep Notes

1.  **"Uniqueness" Problems Mean Hash Sets:** When you see a problem that involves checking for duplicates, uniqueness, or counting frequencies (like "Valid Anagram"), your first thought should be a hash map or a hash set. This is a crucial and extremely common interview pattern.

2.  **Always Discuss Trade-Offs:** Be prepared to explain *why* the hash set is better than the brute-force approach. The key is to articulate the trade-off: we sacrifice some memory (space complexity) to gain a massive improvement in performance (time complexity). This is a classic "space-for-time" trade-off.

3.  **Python's `set()` is Powerful:** A neat Python trick is to compare the length of the original list to the length of a set created from it. If they are not the same length, it means duplicates were removed, and you can solve the problem in one line: `return len(nums) != len(set(nums))`. While clever, make sure you can also code the iterative solution above, as it more clearly demonstrates the underlying logic.
