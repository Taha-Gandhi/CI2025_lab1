# CI2025_lab1
lab 1 Knapsack problem
This project implements a highly efficient, scalable solution for the Multidimensional Multiple Knapsack Problem (MMKP).

The goal is to select a subset of items and assign each chosen item to at most one of the available knapsacks, maximizing the total value, while ensuring all capacity constraints for all knapsacks and all resource dimensions are respected.

Since this problem is computationally hard (NP-hard), especially with large data (thousands of items, many knapsacks), we use an Optimized Greedy Heuristic to find a very good (near-optimal) solution in seconds, where an exact method (like Dynamic Programming) would take hours or days.

## ❓ The Problem

Imagine you have:

1.  **Items:** Each has a `Value` and requires multiple `Weights` (e.g., space, time, budget).
2.  **Knapsacks:** Multiple containers, each with a `Capacity` limit for *each* required weight dimension.

The challenge is to fill these knapsacks to get the highest total value without overfilling any knapsack in *any* dimension.

### Problem Inputs (Data Structures)

| Variable | Description | Shape (Example) |
| :--- | :--- | :--- |
| `values` | 1D array of profit/value for each item. | `(NUM_ITEMS,)` |
| `weights_matrix` | 2D array of resource requirements for each item. | `(NUM_ITEMS, NUM_DIMENSIONS)` |
| `constraints_matrix` | 2D array of max capacity for each knapsack/dimension. | `(NUM_KNAPSACKS, NUM_DIMENSIONS)` |

---
## 💡 The Solution: Optimized Greedy Heuristic

To achieve speed and scalability, the problem is solved using an **Optimized Greedy Heuristic** which uses two key rules:

### 1. Item Selection Rule (Sorting)

Items are prioritized based on their **Profit-to-Average-Weight Ratio** ($\text{Value} / \text{Average Weight}$). This ensures we attempt to place the most "efficient" items first.

### 2. Assignment Rule (Tie-Breaking)

When an item is ready to be assigned, it is placed in the feasible knapsack (fits in all dimensions) that maximizes the **total remaining capacity** afterward. This rule prevents capacity fragmentation, improving the chance of fitting future high-value items.

---
## 🛠 Python Implementation (`knapsack.ipynb`)

This section contains the two core functions: the solver and the validator.

### Solver Function (Optimized Greedy)

def solve_multidimensional_multiple_knapsack_greedy_optimized(
    weights_matrix: np.ndarray, 
    values: np.ndarray, 
    constraints_matrix: np.ndarray
) -> Tuple[float, np.ndarray]
This returns the final value of all the items in all the knapsacks as well as the matrix which clearly says True/False for each item present in the knapsack at most once.

### Validator Function 

def validate_multiple_knapsack_solution(
    solution: np.ndarray, 
    weights_matrix: np.ndarray, 
    constraints_matrix: np.ndarray
) -> Tuple[bool, str] 
This final check is essential to guarantee that the fast, heuristic approach did not accidentally violate any of the strict rules of the MMKP.
