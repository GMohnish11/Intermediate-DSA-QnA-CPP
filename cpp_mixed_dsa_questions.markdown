# Intermediate Mixed DSA Questions and Solutions in C++

This repository contains a collection of intermediate-level Data Structures and Algorithms (DSA) problems in C++, covering arrays, strings, linked lists, stacks, and trees. Designed for coding interview preparation and competitive programming, each problem includes a description, a C++ solution, and an explanation. Authored by Mohnish Gupta, this is ideal for students and developers honing their DSA skills.

## Table of Contents
1. [Find First and Last Position of Element in Sorted Array](#find-first-and-last-position-of-element-in-sorted-array)
2. [Valid Parentheses](#valid-parentheses)
3. [Add Two Numbers (Linked List)](#add-two-numbers-linked-list)
4. [Minimum Path Sum in Grid](#minimum-path-sum-in-grid)
5. [Validate Binary Search Tree](#validate-binary-search-tree)

---

## Find First and Last Position of Element in Sorted Array

### Problem
Given a sorted array of integers and a target value, find the first and last position of the target in the array. Return `[-1, -1]` if the target is not found. For example, if `arr = [5, 7, 7, 8, 8, 10]` and `target = 8`, return `[3, 4]`.

### Solution
```cpp
#include <vector>
std::vector<int> searchRange(std::vector<int>& nums, int target) {
    std::vector<int> result = {-1, -1};
    int n = nums.size();
    
    // Find first position
    int left = 0, right = n - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            result[0] = mid;
            right = mid - 1; // Continue searching left
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    // Find last position
    left = 0; right = n - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            result[1] = mid;
            left = mid + 1; // Continue searching right
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return result;
}
```

### Explanation
- **Approach**: Use binary search twice: once to find the first occurrence by continuing left when the target is found, and once to find the last by continuing right.
- **Time Complexity**: O(log n), two binary searches.
- **Space Complexity**: O(1), constant space.
- **Edge Cases**: Handles empty arrays, no target, or single-element arrays.

---

## Valid Parentheses

### Problem
Given a string containing only parentheses characters (`'(', ')', '{', '}', '[', ']'`), determine if the string is valid (i.e., parentheses are properly nested and closed). For example, if `s = "()[]{}"`, return `true`; if `s = "(]"`, return `false`.

### Solution
```cpp
#include <string>
#include <stack>
bool isValid(std::string s) {
    std::stack<char> stack;
    for (char c : s) {
        if (c == '(' || c == '{' || c == '[') {
            stack.push(c);
        } else {
            if (stack.empty()) return false;
            char top = stack.top();
            stack.pop();
            if ((c == ')' && top != '(') || 
                (c == '}' && top != '{') || 
                (c == ']' && top != '[')) {
                return false;
            }
        }
    }
    return stack.empty();
}
```

### Explanation
- **Approach**: Use a stack to track opening brackets. For each closing bracket, check if it matches the top of the stack. Ensure the stack is empty at the end.
- **Time Complexity**: O(n), single pass through the string.
- **Space Complexity**: O(n), for the stack.
- **Edge Cases**: Handles empty strings, unmatched brackets, or single brackets.

---

## Add Two Numbers (Linked List)

### Problem
Given two non-empty linked lists representing non-negative integers (digits in reverse order), add the numbers and return the result as a linked list. For example, if `l1 = 2 -> 4 -> 3` (342) and `l2 = 5 -> 6 -> 4` (465), return `7 -> 0 -> 8` (807).

### Solution
```cpp
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    ListNode dummy(0);
    ListNode* curr = &dummy;
    int carry = 0;
    
    while (l1 || l2 || carry) {
        int sum = carry;
        if (l1) {
            sum += l1->val;
            l1 = l1->next;
        }
        if (l2) {
            sum += l2->val;
            l2 = l2->next;
        }
        carry = sum / 10;
        curr->next = new ListNode(sum % 10);
        curr = curr->next;
    }
    
    return dummy.next;
}
```

### Explanation
- **Approach**: Traverse both lists, add corresponding digits with carry, and create a new linked list for the result. Handle carry propagation.
- **Time Complexity**: O(max(n, m)), where `n` and `m` are list lengths.
- **Space Complexity**: O(max(n, m)), for the output list.
- **Edge Cases**: Handles lists of different lengths or carry at the end.

---

## Minimum Path Sum in Grid

### Problem
Given an `m x n` grid of non-negative integers, find the minimum path sum from top-left to bottom-right, moving only right or down. For example, if `grid = [[1, 3, 1], [1, 5, 1], [4, 2, 1]]`, the result is `7` (path: 1 -> 3 -> 1 -> 1 -> 1).

### Solution
```cpp
#include <vector>
int minPathSum(std::vector<std::vector<int>>& grid) {
    int m = grid.size(), n = grid[0].size();
    std::vector<std::vector<int>> dp(m, std::vector<int>(n, 0));
    dp[0][0] = grid[0][0];
    
    // Initialize first row and column
    for (int i = 1; i < m; i++) dp[i][0] = dp[i-1][0] + grid[i][0];
    for (int j = 1; j < n; j++) dp[0][j] = dp[0][j-1] + grid[0][j];
    
    // Fill dp table
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            dp[i][j] = std::min(dp[i-1][j], dp[i][j-1]) + grid[i][j];
        }
    }
    
    return dp[m-1][n-1];
}
```

### Explanation
- **Approach**: Use dynamic programming. Create a `dp` table where `dp[i][j]` is the minimum path sum to `(i, j)`. Compute by taking the minimum of the paths from above or left.
- **Time Complexity**: O(m * n), filling the `dp` table.
- **Space Complexity**: O(m * n), for the `dp` table.
- **Edge Cases**: Handles single-row or single-column grids.

---

## Validate Binary Search Tree

### Problem
Given a binary tree, determine if it is a valid Binary Search Tree (BST), where for each node, all nodes in the left subtree are less than the node, and all nodes in the right subtree are greater. For example, `[2, 1, 3]` is valid, but `[5, 1, 4, null, null, 3, 6]` is not.

### Solution
```cpp
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

bool isValidBST(TreeNode* root) {
    return isValidBSTHelper(root, LONG_MIN, LONG_MAX);
}

bool isValidBSTHelper(TreeNode* node, long min, long max) {
    if (!node) return true;
    if (node->val <= min || node->val >= max) return false;
    return isValidBSTHelper(node->left, min, node->val) && 
           isValidBSTHelper(node->right, node->val, max);
}
```

### Explanation
- **Approach**: Use recursive validation with range checking. Each node must lie within a valid range (`min`, `max`), updated for left and right subtrees.
- **Time Complexity**: O(n), visiting each node once.
- **Space Complexity**: O(h), where `h` is the tree height, due to recursion stack.
- **Edge Cases**: Handles empty trees, single-node trees, or invalid BSTs due to duplicate values.

---

## How to Run
1. Clone the repository:
   ```bash
   git clone https://github.com/GMohnish11/CPP-Mixed-DSA-Questions.git
   cd CPP-Mixed-DSA-Questions
   ```
2. Compile and run a solution:
   ```bash
   g++ solutions/solution1_search_range.cpp -o search_range
   ./search_range
   ```
3. Use `main.cpp` to test solutions with custom inputs:
   ```cpp
   #include <vector>
   #include <iostream>
   #include "solutions/solution1_search_range.cpp"
   int main() {
       std::vector<int> nums = {5, 7, 7, 8, 8, 10};
       int target = 8;
       auto result = searchRange(nums, target);
       std::cout << "[" << result[0] << ", " << result[1] << "]" << std::endl; // Output: [3, 4]
       return 0;
   }
   ```

## Directory Structure
```
├── solutions/
│   ├── solution1_search_range.cpp      # Find first and last position
│   ├── solution2_valid_parentheses.cpp # Valid parentheses
│   ├── solution3_add_numbers.cpp       # Add two numbers (linked list)
│   ├── solution4_min_path_sum.cpp      # Minimum path sum in grid
│   ├── solution5_valid_bst.cpp         # Validate binary search tree
├── main.cpp                           # Driver code to test solutions
├── cpp_mixed_dsa_questions.md         # This file
├── README.md                          # Repository overview
```

## Contributing
Contributions are welcome! To contribute:
1. Fork the repository.
2. Create a branch: `git checkout -b feature/new-problem`.
3. Add your problem and solution in `solutions/` and update `cpp_mixed_dsa_questions.md`.
4. Commit changes: `git commit -m "Add new DSA problem"`.
5. Push: `git push origin feature/new-problem`.
6. Submit a Pull Request.

Report issues via the [Issues](https://github.com/GMohnish11/CPP-Mixed-DSA-Questions/issues) tab.

## Acknowledgments
- **Author**: Mohnish Gupta
- **Institution**: St. Peter's Engineering College, Hyderabad
- **Inspiration**: Competitive programming platforms like LeetCode, HackerRank, and GeeksforGeeks
- **Resources**: C++ Standard Library and DSA references