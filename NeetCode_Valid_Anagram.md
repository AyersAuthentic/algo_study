## 📝 NeetCode: Valid Anagram

  * **Date Solved:** September 29, 2025
  * **Link:** [Valid Anagram](https://leetcode.com/problems/valid-anagram/)

-----

### \#\# 🎯 Problem Summary

The goal is to determine if two strings, `s` and `t`, are anagrams of each other. An anagram is a word or phrase formed by rearranging the letters of another, such as "cinema," formed from "iceman." This means they must contain the exact same characters with the exact same frequencies.

-----

### \#\# 🧠 Key Concepts Tested

This is a classic frequency counting problem, making it a perfect test of your ability to use hash maps.

  * **Hash Maps (Dictionaries):** The ideal data structure for efficiently storing and retrieving key-value pairs, in this case, character-frequency counts.
  * **Frequency Counting:** The core algorithmic pattern of counting the occurrences of items in a collection.
  * **Time & Space Complexity Analysis:** Evaluating the efficiency of different approaches.

-----

### \#\# ✅ Solution Approaches

#### \#\#\# Approach 1: Two Hash Maps

This approach is very clear and directly follows the definition of an anagram: create a frequency map for each string and then check if the maps are identical.

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        # Anagrams must have the same length.
        if len(s) != len(t):
            return False

        # Initialize two hash maps (dictionaries).
        countS, countT = {}, {}

        # Build the frequency map for both strings in one loop.
        for i in range(len(s)):
            countS[s[i]] = 1 + countS.get(s[i], 0)
            countT[t[i]] = 1 + countT.get(t[i], 0)
        
        # In Python, two dictionaries are equal if they have the
        # same keys and the same corresponding values.
        return countS == countT
```

  * **Time Complexity: $O(n)$** - We iterate through the strings of length *n* once.
  * **Space Complexity: $O(n)$** - In the worst case, we store two hash maps, each containing up to *n* unique characters.

#### \#\#\# Approach 2: One Hash Map (Space Optimized)

A more space-efficient method is to use a single hash map. We build the frequency map from the first string and then "tear it down" using the second string.

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        counts = {}

        # Increment counts for string s
        for char in s:
            counts[char] = 1 + counts.get(char, 0)
        
        # Decrement counts for string t
        for char in t:
            # If a character is not in the map or its count is zero,
            # it means t has an extra character or an imbalance.
            if counts.get(char, 0) == 0:
                return False
            counts[char] -= 1
        
        return True
```

  * **Time Complexity: $O(n)$** - We still iterate through the strings.
  * **Space Complexity: $O(n)$** - We only store one hash map, using half the space of the first approach.

-----

### \#\# 💡 Key Takeaways & Interview Prep Notes

1.  **"Frequency Counting" Screams "Hash Map":** This is a primary pattern. When a problem mentions anagrams, duplicates, or counting character occurrences, a hash map is almost always the right tool.

2.  **Master `dict.get(key, default)`:** This method is your best friend when counting with standard dictionaries. The pattern `count[key] = 1 + count.get(key, 0)` is a clean and efficient way to handle both existing and new keys without needing an `if/else` check.

3.  **Know Your Language's Features:** The ability to compare two dictionaries directly with `countS == countT` in Python (as shown in Approach 1) is a powerful shortcut. Knowing these features makes for cleaner code.

4.  **Discuss Trade-Offs:** Both solutions are valid and have the same time complexity. Being able to discuss why Approach 2 is more space-efficient is a sign of a strong candidate. You can explain that it avoids storing a redundant second map.
