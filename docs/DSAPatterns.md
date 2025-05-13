# Key Coding Interview Patterns

After solving a lot of DSA problems, I’ve noticed some key patterns that are important for coding interviews.

At the end of this article, I have also included links to some of the best LeetCode articles that I found helpful for better understanding.

---

## 1. Fast and Slow Pointer

**Description:** This technique uses two pointers moving at different speeds to solve problems involving cycles, such as finding the middle of a list, detecting loops, or checking for palindromes.

- Linked List Cycle II  
- Remove nth Node from the End of List  
- Find the Duplicate Number  
- Palindrome Linked List

---

## 2. Overlapping Intervals

**Description:** Intervals are often manipulated through sorting and merging based on their start and end times.

- Merge Intervals  
- Insert Interval  
- My Calendar II  
- Minimum Number of Arrows to Burst Balloons  
- Non-overlapping Intervals

---

## 3. Prefix Sum

**Description:** Prefix Sums/Products store cumulative sums or products to allow quick subarray range queries.

- Find the Middle Index in Array  
- Product of Array Except Self  
- Maximum Product Subarray  
- Number of Ways to Split Array  
- Range Sum Query 2D

---

## 4. Sliding Window

**Description:** A subarray/substring that "slides" over the input to solve problems in linear time.

### Fixed Size
- Maximum Sum Subarray of Size K  
- Number of Subarrays Having Average ≥ Threshold  
- Repeated DNA Sequences  
- Permutation in String  
- Sliding Subarray Beauty  
- Sliding Window Maximum

### Variable Size
- Longest Substring Without Repeating Characters  
- Minimum Size Subarray Sum  
- Subarray Product Less Than K  
- Max Consecutive Ones  
- Fruits Into Baskets  
- Count Number of Nice Subarrays  
- Minimum Window Substring

---

## 5. Two Pointers

**Description:** Two indices move at different speeds to solve array/linked list problems.

- Two Sum II - Input Array is Sorted  
- Sort Colors (Dutch National Flag)  
- Next Permutation  
- Bag of Tokens  
- Container With Most Water  
- Trapping Rain Water

---

## 6. Cyclic Sort (Index-Based)

**Description:** Efficient for placing consecutive numbers in correct positions.

- Missing Number  
- Find Missing Numbers  
- Set Mismatch  
- First Missing Positive

---

## 7. Reversal of Linked List (In-place)

**Description:** Reverse a linked list without extra space.

- Reverse Linked List  
- Reverse Nodes in k-Group  
- Swap Nodes in Pairs

---

## 8. Matrix Manipulation

**Description:** Use row-column traversal or matrix property-based logic.

- Rotate Image  
- Spiral Matrix  
- Set Matrix Zeroes  
- Game of Life

---

## 9. Breadth First Search (BFS)

**Description:** Level-order exploration using a queue.

- Shortest Path in Binary Matrix  
- Rotten Oranges  
- As Far From Land as Possible  
- Word Ladder

---

## 10. Depth First Search (DFS)

**Description:** Explore as far as possible before backtracking.

- Number of Closed Islands  
- Coloring a Border  
- Number of Enclaves  
- Time Needed to Inform All Employees  
- Find Eventual Safe States

---

## 11. Backtracking

**Description:** Explore all potential solutions for puzzles and path-finding.

- Permutation II  
- Combination Sum  
- Generate Parenthesis  
- N-Queens  
- Sudoku Solver  
- Palindrome Partitioning  
- Word Search

---

## 12. Modified Binary Search

**Description:** Apply binary search on rotated/special conditions.

- Search in Rotated Sorted Array  
- Find Minimum in Rotated Sorted Array  
- Find Peak Element  
- Single Element in a Sorted Array  
- Minimum Time to Arrive on Time  
- Capacity to Ship Packages Within 'D' Days  
- Koko Eating Bananas  
- Find in Mountain Array  
- Median of Two Sorted Arrays

---

## 13. Bitwise XOR

**Description:** Solve problems like finding single elements and pairings.

- Missing Number  
- Single Number II  
- Single Number III  
- Find the Original Array of Prefix XOR  
- XOR Queries of a Subarray

---

## 14. Top 'K' Elements

**Description:** Use heaps or quickselect.

- Top K Frequent Elements  
- Kth Largest Element  
- Ugly Number II  
- K Closest Points to Origin

---

## 15. K-way Merge

**Description:** Merge multiple sorted lists using a heap.

- Find K Pairs with Smallest Sums  
- Kth Smallest Element in a Sorted Matrix  
- Merge K Sorted Lists  
- Smallest Range Covering Elements from K Lists

---

## 16. Two Heaps

**Description:** Use max heap + min heap for median/dynamic data tracking.

- Find Median from Data Stream  
- Sliding Window Median  
- IPO

---

## 17. Monotonic Stack

**Description:** Solve range queries with increasing/decreasing stacks.

- Next Greater Element II  
- Next Greater Node in Linked List  
- Daily Temperatures  
- Online Stock Span  
- Maximum Width Ramp  
- Largest Rectangle in Histogram

---

## 18. Trees

### Level Order (BFS)
- Level Order Traversal  
- Zigzag Level Order Traversal  
- Even Odd Tree  
- Reverse Odd Levels  
- Deepest Leaves Sum  
- Add One Row to Tree  
- Maximum Width of Binary Tree  
- All Nodes Distance K in Binary Tree

### Tree Construction
- Construct BT from Preorder and Inorder  
- Construct BT from Postorder and Inorder  
- Maximum Binary Tree  
- Construct BST from Preorder

### Height-Related
- Maximum Depth of BT  
- Balanced Binary Tree  
- Diameter of Binary Tree  
- Minimum Depth of BT

### Root to Leaf Paths
- Binary Tree Paths  
- Path Sum II  
- Sum Root to Leaf Numbers  
- Smallest String Starting from Leaf  
- Insufficient Nodes in Root to Leaf  
- Pseudo-Palindromic Paths in Binary Tree  
- Binary Tree Maximum Path Sum

### Ancestor Problems
- LCA of Binary Tree  
- Max Difference Between Node and Ancestor  
- LCA of Deepest Leaves  
- Kth Ancestor of a Tree Node

### Binary Search Tree
- Validate BST  
- Range Sum of BST  
- Minimum Absolute Difference in BST  
- Insert into a BST  
- LCA of BST

---

## 19. Dynamic Programming (DP)

### Take / Not Take (0/1 Knapsack)
- House Robber II  
- Target Sum  
- Partition Equal Subset Sum  
- Ones and Zeroes  
- Last Stone Weight II

### Infinite Supply
- Coin Change  
- Coin Change II  
- Perfect Squares  
- Minimum Cost For Tickets

### Longest Increasing Subsequence
- Longest Increasing Subsequence  
- Largest Divisible Subset  
- Maximum Length of Pair Chain  
- Number of LIS  
- Longest String Chain

### DP on Grids
- Unique Paths II  
- Minimum Path Sum  
- Triangle  
- Minimum Falling Path Sum  
- Maximal Square  
- Cherry Pickup  
- Dungeon Game

### DP on Strings
- Longest Common Subsequence  
- Longest Palindromic Subsequence  
- Palindromic Substrings  
- Longest Palindromic Substring  
- Edit Distance  
- Minimum ASCII Delete Sum for Two Strings  
- Distinct Subsequences  
- Shortest Common Supersequence  
- Wildcard Matching

### DP on Stocks
- Buy and Sell Stocks II  
- Buy and Sell Stocks III  
- Buy and Sell Stocks IV  
- Buy and Sell with Cooldown  
- Buy and Sell with Transaction Fee

### Partition DP (MCM)
- Partition Array for Maximum Sum  
- Burst Balloons  
- Minimum Cost to Cut a Stick  
- Palindrome Partitioning II

---

## 20. Graphs

### Topological Sort (DAG)
- Course Schedule  
- Course Schedule II  
- Strange Printer II  
- Sequence Reconstruction  
- Alien Dictionary

### Union Find (Disjoint Set)
- Number of Operations to Make Network Connected  
- Redundant Connection  
- Accounts Merge  
- Satisfiability of Equality Equations

### Graph Algorithms
- Kruskal's: Minimum Cost to Connect All Points  
- Dijkstra's: Cheapest Flights Within K Stops  
- Floyd-Warshall: City with Smallest #Neighbors at Threshold  
- Bellman-Ford: Network Delay Time

---

## 21. Greedy

**Description:** Make the best choice at every step.

- Jump Game II  
- Gas Station  
- Bag of Tokens  
- Boats to Save People  
- Wiggle Subsequence  
- Car Pooling  
- Candy

---

## 22. Design Data Structures

**Description:** Build optimized data structures for custom operations.

- Design Twitter  
- Design Browser History  
- Design Circular Deque  
- Snapshot Array  
- LRU Cache  
- LFU Cache

---

## Useful LeetCode Articles

- **Two Pointers**  
  - Solved all Two Pointers problems in 100 days  
- **Sliding Window**  
  - Sliding Window Technique and Question Bank  
  - C++ Maximum Sliding Window Cheatsheet Template!  
- **Greedy**  
  - Greedy for Beginners: Problems & Sample Solutions  
  - Top Greedy Questions  
- **Linked List**  
  - Become Master in Linked List  
  - Must-Do LinkedList Problems on LeetCode  
- **Trees**  
  - Tree Question Pattern | 2021 Placement  
  - Master Tree Patterns  
- **Binary Search**  
  - 5 Variations of Binary Search  
  - Binary Search for Beginners: Problems & Patterns  
- **Dynamic Programming (DP)**  
  - Dynamic Programming Patterns  
  - DP for Beginners: Problems & Patterns  
- **Graphs**  
  - Graph for Beginners  
  - Become Master in Graph  
  - Graph algorithms + problems to practice  
- **Bit Manipulation**  
  - Bit Manipulation Problem Solving  
  - All Types of Bit Manipulation Patterns and How to Use

---
