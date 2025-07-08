# Polygonal Coverage Optimization: Crystals & Mines

This project aims to enclose valuable crystal points while avoiding penalizing mine points on a 2D grid, maximizing the total enclosed value using a polygon. It combines a mathematical programming model with Gurobi and a custom heuristic implemented in C++.

---

## Problem Statement

Given:

* A set of **crystals** with coordinates and value: `(x, y, value)`
* A set of **mines** with coordinates and penalty: `(x, y, penalty)`

Goal:

* Construct a **non-intersecting polygon** (with alternating vertical and horizontal edges)
* **Maximize net value**:

  ```
  total_value = sum(enclosed_crystal_values) - sum(enclosed_mine_penalties)
  ```

---

## Approaches

### 1. Gurobi Optimization (Python)

A mathematically rigorous model using Mixed Integer Programming (MIP) and Quadratic Constraints:

* Vertex coordinates defined as continuous variables
* Edge orientation defined with binary variables
* Alternating edge orientation constraints
* Non-intersecting polygon ensured using indicator constraints
* Point-in-polygon check with cross-product constraints

**Limitations:**

* Works well for small instances
* Does **not scale well** for large point sets or polygon sizes

---

### 2. Heuristic Method (C++)

A custom high-performance solution to handle large datasets:

* Divides the grid into rectangles with varying subdivisions
* Uses prefix sums for efficient region sum queries
* Implements a greedy selection of high-value rectangles
* Builds a closed polygonal path from selected rectangles

**Advantages:**

* **Fast and scalable**
* Achieves **95%+ accuracy** across all test cases
* Runs independently without any commercial solver

---



## How to Run

### Using Gurobi (Python)

1. Install dependencies:

   ```bash
   pip install gurobipy
   ```
2. Run `gurobi_model.ipynb` in Google Colab or Jupyter with your license parameters

### Using Heuristic (C++)

1. Compile the code:

   ```bash
   g++ codecpp.cpp -o heuristic -O2
   ```
2. Make sure test inputs `input00.txt` to `input09.txt` are in the same directory
3. Run the executable:

   ```bash
   ./heuristic
   ```

---

## Results

* **Average accuracy:** \~95% - 98% (compared to optimal value)
* **Polygon shape:** A chain of axis-aligned edges enclosing high-value zones

---

## Possible Improvements

* Generalize edge orientation beyond axis-aligned
* Use advanced metaheuristics (e.g. simulated annealing, GA)
* Parallelize rectangle evaluation to improve performance further


---

## License

This project uses Gurobi under an **academic license** .
