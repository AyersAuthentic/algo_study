## 📝 A Step-by-Step Guide for Solving Algorithm Problems

This framework is based on George Pólya's four-step process. Following these steps will help you stay calm and structured, even on a daunting problem.

### ## Step 1: Understand the Problem

Before writing any code, you must deeply understand the goal. In an interview, this is also how you start the conversation.

1.  **Restate the Prompt in Your Own Words:** Tell the interviewer what you think the goal is. "So, if I'm understanding correctly, we're given an array of integers, and we need to find the two numbers that add up to a specific target. Is that right?"
2.  **Clarify Inputs, Outputs, and Constraints:** Ask questions to uncover the boundaries of the problem.
    * **Inputs:** "What's the format of the input? An array of numbers? A string?"
    * **Outputs:** "What should I return? A boolean? An array of indices?"
    * **Constraints:** "How large can the input array be? Can the numbers be negative?"
3.  **Identify Edge Cases:** Think about the tricky inputs.
    * What if the input is empty, `null`, or has only one element?
    * What if all the elements are the same?
    * What if there's no valid solution?

---

### ## Step 2: Devise a Plan

This is where you strategize. Don't jump to the "perfect" solution immediately.

1.  **Start with the Brute-Force Solution:** Always begin with the most obvious, even if it's slow. This proves you can solve the problem correctly. Verbalize this plan. "My first thought is a brute-force approach. I could use two nested loops to check every pair of numbers. This would be $O(n^2)$, but it would guarantee a correct answer."
2.  **Find the Bottleneck:** Analyze your brute-force plan. Where is the inefficiency? It's almost always in the repeated work (the nested loop).
3.  **Brainstorm Optimizations:** Think about your patterns and data structures. "The bottleneck is that for each number, we're slowly searching the rest of the array. How can we make that search faster? We could use a **Hash Map** to store numbers we've seen, which would make the lookup $O(1)$."
4.  **State Your Optimal Plan:** Clearly outline the new, better approach to your interviewer *before* you start coding. "Okay, my optimal plan is to iterate through the array once. For each number, I'll check if its complement is in my hash map. If it is, I've found the solution. If not, I'll add the current number to the hash map and continue."

---

### ## Step 3: Carry Out the Plan (Implement)

Now you can write the code for your optimal plan.

1.  **Narrate as You Code:** Talk through your logic as you type. This keeps the interviewer engaged and allows them to follow your thought process. "First, I'll initialize an empty hash map called `seen`. Now, I'll start my loop..."
2.  **Write Clean Code:** Use descriptive variable names (`seen`, `complement`) instead of single letters (`x`, `y`).

---

### ## Step 4: Look Back (Review and Verify)

Don't just say "I'm done" when you finish typing. Review your work.

1.  **Manually Test Your Code:** Pick an example input and walk through your code line-by-line, tracking the values of your variables. "Let's trace this with the input `[2, 7, 11]` and a `target` of `9`..."
2.  **Test with Your Edge Cases:** "What happens if the input is an empty array? My code handles this; the loop won't run, and it will return the default value."
3.  **State the Complexity:** Clearly state the final time and space complexity. "This solution has a time complexity of $O(n)$ because we iterate through the array once, and a space complexity of $O(n)$ because, in the worst case, the hash map will store all *n* elements."
