# CPP-DSA-Questions

## Overview
This repository, `CPP-Mixed-DSA-Questions`, contains a collection of intermediate-level Data Structures and Algorithms (DSA) problems in C++, developed by Mohnish Gupta. Covering arrays, strings, linked lists, stacks, and trees, it includes problems like finding element positions, validating parentheses, and checking BSTs. Designed for coding interview preparation and competitive programming, it offers detailed explanations and efficient C++ code.

## Description
A collection of intermediate C++ DSA problems with solutions, covering arrays, strings, linked lists, stacks, and trees. Ideal for coding practice and interviews, by Mohnish Gupta.

## Features
- **Mixed DSA Problems**: Includes problems on arrays, strings, linked lists, stacks, and trees, such as binary search, stack-based validation, and tree traversal.
- **C++ Solutions**: Efficient, well-commented code using modern C++ (e.g., `std::vector`, `std::stack`, `struct TreeNode`).
- **Explanations**: Each problem includes a description, solution, time/space complexity, and edge case analysis in `cpp_mixed_dsa_questions.md`.
- **Testable Code**: Includes a `main.cpp` driver file to test solutions with custom inputs.
- **Modular Design**: Solutions are organized in `solutions/` for easy integration and testing.

## Installation
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/GMohnish11/CPP-Mixed-DSA-Questions.git
   cd CPP-Mixed-DSA-Questions
   ```
2. **Ensure C++ Compiler**:
   - Install a C++ compiler (e.g., `g++` via GCC) if not already present.
   - Verify: `g++ --version`.
3. **Compile and Run**:
   - Compile a specific solution:
     ```bash
     g++ solutions/solution1_search_range.cpp -o search_range
     ./search_range
     ```
   - Or use `main.cpp` to test all solutions:
     ```bash
     g++ main.cpp -o test
     ./test
     ```

## Usage
### Exploring Problems
- Read `cpp_mixed_dsa_questions.md` for problem descriptions, solutions, and explanations.
- Problems include:
  1. Find First and Last Position of Element in Sorted Array
  2. Valid Parentheses
  3. Add Two Numbers (Linked List)
  4. Minimum Path Sum in Grid
  5. Validate Binary Search Tree

### Running Solutions
- Each solution is in the `solutions/` directory (e.g., `solution1_search_range.cpp`).
- Modify `main.cpp` to test different inputs:
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
- Compile and run as shown in the Installation section.

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
├── README.md                          # This file
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
