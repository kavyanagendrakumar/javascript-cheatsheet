# DSA Patterns You Need To Know by Anubhav (x7og)

Hey LeetCoders,

I'm Anubhav, and I'm thrilled to share a comprehensive guide to DSA patterns that are crucial for acing coding interviews. Understanding these patterns can transform your problem-solving approach, making complex problems feel more manageable. Let's dive in!

---

## 1. Sliding Window

**Description:**
The Sliding Window pattern is used to perform a required operation on a specific window size of a given array or linked list. It involves creating a window that can either be of a fixed or variable size, and this window "slides" over the data.

**When to use:**
*   When the problem involves a contiguous subarray or substring.
*   When you need to find the min/max/average or some other property of a subarray/substring of a fixed or variable size.
*   Problems asking for the longest/shortest subarray/substring satisfying certain conditions.

**Common Problems:**
*   [Maximum Sum Subarray of Size K](https://leetcode.com/problems/maximum-subarray/) (Note: Original problem is general, size K is a variant)
*   [Smallest Subarray with a Greater Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)
*   [Longest Substring with K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/)
*   [Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/)
*   [No-repeat Substring](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
*   [Longest Substring with Same Letters after Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)
*   [Longest Subarray with Ones after Replacement](https://leetcode.com/problems/max-consecutive-ones-iii/)

---

## 2. Two Pointers

**Description:**
The Two Pointers pattern uses two pointers to iterate through an array or list until the pointers meet or satisfy a certain condition. These pointers can move towards each other, away from each other, or in the same direction.

**When to use:**
*   Problems involving sorted arrays or linked lists where you need to find a pair, triplet, or subsegment.
*   When you need to compare elements from both ends of an array or from different positions simultaneously.
*   Problems that can be solved by processing the array from two different directions.

**Common Problems:**
*   [Pair with Target Sum](https://leetcode.com/problems/two-sum/) (Sorted array variant)
*   [Remove Duplicates](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
*   [Squaring a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)
*   [Triplet Sum to Zero](https://leetcode.com/problems/3sum/)
*   [Triplet Sum Close to Target](https://leetcode.com/problems/3sum-closest/)
*   [Subarrays with Product Less than a Target](https://leetcode.com/problems/subarray-product-less-than-k/)
*   [Dutch National Flag Problem](https://leetcode.com/problems/sort-colors/)

---

## 3. Fast & Slow Pointers (Hare & Tortoise)

**Description:**
This pattern uses two pointers that move through a sequence (like a linked list or array) at different speeds. The fast pointer moves more steps per iteration than the slow pointer.

**When to use:**
*   Detecting cycles in a linked list or array.
*   Finding the middle element of a linked list.
*   Problems where you need to determine a position relative to the end of a list without knowing its length.

**Common Problems:**
*   [LinkedList Cycle](https://leetcode.com/problems/linked-list-cycle/)
*   [Start of LinkedList Cycle](https://leetcode.com/problems/linked-list-cycle-ii/)
*   [Happy Number](https://leetcode.com/problems/happy-number/)
*   [Middle of the LinkedList](https://leetcode.com/problems/middle-of-the-linked-list/)

---

## 4. Merge Intervals

**Description:**
The Merge Intervals pattern is used to deal with overlapping intervals. Given two intervals (‘a’ and ‘b’), there will be six different ways the two intervals can relate to each other.

**When to use:**
*   Problems involving merging, inserting, or finding intersections of intervals.
*   When you need to consolidate a list of time periods or ranges.

**Common Problems:**
*   [Merge Intervals](https://leetcode.com/problems/merge-intervals/)
*   [Insert Interval](https://leetcode.com/problems/insert-interval/)
*   [Intervals Intersection](https://leetcode.com/problems/interval-list-intersections/)
*   [Conflicting Appointments](https://leetcode.com/problems/meeting-rooms-ii/) (Checking if any appointments conflict is Meeting Rooms I, finding min rooms is Meeting Rooms II)

---

## 5. Cyclic Sort

**Description:**
This pattern is used to deal with problems involving arrays containing numbers in a given range (e.g., 1 to N). The idea is to iterate through the array and if the current number is not at its correct index, swap it with the number at its correct index.

**When to use:**
*   Problems involving a sorted array with numbers in a definite range (e.g., 1 to n).
*   Finding missing numbers, duplicate numbers, or the smallest missing positive number in an unsorted array.

**Common Problems:**
*   [Cyclic Sort](https://leetcode.com/problems/missing-number/) (Conceptual problem, Missing Number is an application)
*   [Find the Missing Number](https://leetcode.com/problems/missing-number/)
*   [Find all Missing Numbers](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)
*   [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)
*   [Find all Duplicate Numbers](https://leetcode.com/problems/find-all-duplicates-in-an-array/)

---

## 6. In-place Reversal of a LinkedList

**Description:**
This pattern is used to reverse the links between nodes of a linked list in-place, i.e., without using extra space. Often, three pointers are used: `previous`, `current`, and `next`.

**When to use:**
*   When you need to reverse a linked list or parts of it.
*   Problems that require processing a linked list in reverse order.

**Common Problems:**
*   [Reverse a LinkedList](https://leetcode.com/problems/reverse-linked-list/)
*   [Reverse a Sub-list](https://leetcode.com/problems/reverse-linked-list-ii/)
*   [Reverse every K-element Sub-list](https://leetcode.com/problems/reverse-nodes-in-k-group/)

---

## 7. Tree Breadth-First Search (Tree BFS)

**Description:**
Tree BFS involves traversing a tree level by level. It uses a queue to keep track of nodes at the current level before moving to the next level.

**When to use:**
*   Finding the shortest path between two nodes in a tree.
*   Level order traversal of a tree.
*   Problems where you need to process nodes based on their depth or level.

**Common Problems:**
*   [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)
*   [Reverse Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/)
*   [Zigzag Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)
*   [Level Averages in a Binary Tree](https://leetcode.com/problems/average-of-levels-in-binary-tree/)
*   [Connect Level Order Siblings](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)

---

## 8. Tree Depth-First Search (Tree DFS)

**Description:**
Tree DFS involves traversing a tree by going as deep as possible along each branch before backtracking. It can be implemented using recursion or an explicit stack.

**When to use:**
*   Pathfinding in a tree (e.g., finding a path from root to a specific node).
*   Problems involving tree traversal where order (pre-order, in-order, post-order) is important.
*   Checking structural properties of a tree (e.g., if it's a valid BST).

**Common Problems:**
*   [Binary Tree Path Sum](https://leetcode.com/problems/path-sum/)
*   [All Paths for a Sum](https://leetcode.com/problems/path-sum-ii/)
*   [Sum of Path Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers/)
*   [Path With Given Sequence](https://leetcode.com/problems/check-if-a-string-is-a-valid-sequence-from-root-to-leaves-path-in-a-binary-tree/)
*   [Count Paths for a Sum](https://leetcode.com/problems/path-sum-iii/)

---

## 9. Two Heaps

**Description:**
In many problems where we need to find something among a collection of elements, like the smallest, largest, or median, heaps (or priority queues) can be very useful. If we need to find both, or maintain elements in two sets, the Two Heaps pattern can be applied.

**When to use:**
*   Finding the median of a stream of numbers.
*   Problems where you need to maintain elements in two sets, typically one for smaller halves and one for larger halves.
*   Scheduling problems.

**Common Problems:**
*   [Find the Median of a Number Stream](https://leetcode.com/problems/find-median-from-data-stream/)
*   [Sliding Window Median](https://leetcode.com/problems/sliding-window-median/)
*   [Maximize Capital](https://leetcode.com/problems/ipo/)

---

## 10. Subsets

**Description:**
This pattern deals with generating all possible subsets (or permutations, combinations) of a given set of elements. It often involves backtracking or iterative approaches.

**When to use:**
*   Generating permutations or combinations.
*   Problems that require exploring all possible configurations or groupings of elements.

**Common Problems:**
*   [Subsets](https://leetcode.com/problems/subsets/)
*   [Subsets With Duplicates](https://leetcode.com/problems/subsets-ii/)
*   [Permutations](https://leetcode.com/problems/permutations/)
*   [String Permutations by changing case](https://leetcode.com/problems/letter-case-permutation/)
*   [Balanced Parentheses](https://leetcode.com/problems/generate-parentheses/)
*   [Unique Generalized Abbreviations](https://leetcode.com/problems/generalized-abbreviation/)

---

## 11. Modified Binary Search

**Description:**
This pattern is an extension of the standard Binary Search. It's used when the target element or condition is not straightforward, or the array has some specific properties (e.g., bitonic, rotated).

**When to use:**
*   Searching in sorted arrays where the condition for finding the element is complex.
*   Finding an element in a bitonic array or a rotated sorted array.
*   Problems where the search space can be divided in half based on some property.

**Common Problems:**
*   [Order-agnostic Binary Search](https://leetcode.com/problems/binary-search/) (Standard, but basis for modifications)
*   [Ceiling of a Number](https://leetcode.com/problems/find-smallest-letter-greater-than-target/) (Variant, find number >= target)
*   [Next Letter](https://leetcode.com/problems/find-smallest-letter-greater-than-target/)
*   [Number Range](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
*   [Search in a Sorted Infinite Array](https://leetcode.com/problems/search-in-a-sorted-array-of-unknown-size/)
*   [Search in Rotated Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

---

## 12. Top 'K' Elements

**Description:**
This pattern is used to find the top 'K' (or smallest 'K') elements from a given set. A min-heap or max-heap is often used to efficiently keep track of the 'K' elements.

**When to use:**
*   Finding the K largest/smallest numbers, most frequent numbers, etc.
*   Problems where you need to select a small number of items from a large dataset based on some criteria.

**Common Problems:**
*   [Top 'K' Numbers](https://leetcode.com/problems/kth-largest-element-in-an-array/)
*   [Kth Smallest Number](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/) (or in an unsorted array)
*   ['K' Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)
*   [Connect Ropes (Minimum Cost to Connect Ropes)](https://leetcode.com/problems/minimum-cost-to-connect-sticks/)
*   [Top 'K' Frequent Numbers](https://leetcode.com/problems/top-k-frequent-elements/)
*   [Frequency Sort](https://leetcode.com/problems/sort-characters-by-frequency/)
*   [Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/)

---

## 13. K-way Merge

**Description:**
This pattern is used to merge 'K' sorted lists or arrays into a single sorted list. A min-heap is often used to efficiently get the smallest element among the heads of all 'K' lists.

**When to use:**
*   Merging multiple sorted inputs.
*   Problems involving finding the smallest/largest elements from a combination of sorted lists.

**Common Problems:**
*   [Merge K Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)
*   [Kth Smallest Number in M Sorted Lists](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/) (Can be seen as K-way merge idea)
*   [Kth Smallest Number in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)
*   [Smallest Number Range (covering elements from K lists)](https://leetcode.com/problems/smallest-range-covering-elements-from-k-lists/)

---

## 14. 0/1 Knapsack (Dynamic Programming)

**Description:**
The 0/1 Knapsack pattern is used to solve problems where you need to select items with given weights and values to maximize total value without exceeding a weight capacity. Each item can either be taken or not (0/1). This is a classic DP pattern.

**When to use:**
*   Optimization problems where you have to choose items to maximize/minimize some value under certain constraints.
*   Problems that can be broken down into subproblems of whether to include an item or not.

**Common Problems:**
*   [0/1 Knapsack](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/) (Classic problem, often a basis for LeetCode variants)
*   [Equal Subset Sum Partition](https://leetcode.com/problems/partition-equal-subset-sum/)
*   [Subset Sum](https://leetcode.com/problems/target-sum/) (Can be framed as this)
*   [Minimum Subset Sum Difference](https://leetcode.com/problems/partition-array-into-two-arrays-to-minimize-sum-difference/) (Harder variant)
*   [Count of Subset Sum](https://leetcode.com/problems/target-sum/)
*   [Target Sum](https://leetcode.com/problems/target-sum/)

---

## 15. Topological Sort (Graph)

**Description:**
Topological Sort is used to find a linear ordering of elements that have dependencies on each other. For example, if task A must be completed before task B, then A comes before B in the ordering. It's typically used with Directed Acyclic Graphs (DAGs).

**When to use:**
*   Scheduling tasks with dependencies.
*   Determining the order of compilation of source files.
*   Finding if a graph has a cycle (if topological sort is not possible for all nodes).

**Common Problems:**
*   [Task Scheduling](https://leetcode.com/problems/course-schedule/) (Is it possible to finish all tasks?)
*   [Task Scheduling Order](https://leetcode.com/problems/course-schedule-ii/)
*   [Alien Dictionary](https://leetcode.com/problems/alien-dictionary/)
*   [Reconstructing a Sequence](https://leetcode.com/problems/sequence-reconstruction/)

---

**Conclusion:**

Mastering these DSA patterns will significantly boost your problem-solving skills for coding interviews. Practice problems related to each pattern to solidify your understanding. Remember, pattern recognition is key!

Happy Coding!

**Anubhav (x7og)**

---

**Connect with me:**
*   **LeetCode:** [x7og](https://leetcode.com/u/x7og/)
*   **LinkedIn:** [Anubhav Singh](https://www.linkedin.com/in/anubhavsinghx7og/)
*   **GitHub:** [anubhavsinghx7og](https://github.com/anubhavsinghx7og)
*   **Topmate:** [Anubhav Singh](https://topmate.io/anubhavsingh)
