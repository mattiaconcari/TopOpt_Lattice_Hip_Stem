# 🚀 Stress-Constrained Topology Optimization (Python & Abaqus)

> **⚠️ Confidentiality Note (NDA):** > The full source code, specific CAD models, and proprietary data of this project are bound by an academic/corporate Non-Disclosure Agreement (NDA) and cannot be published. This repository serves as an *architectural portfolio* to showcase the developed methodologies, the technical challenges overcome, and the technology stack used.

## 📌 Project Description
This thesis project focuses on the development of an automated framework for **Stress-Constrained Topology Optimization**. 
The main objective is to maximize compliance (making the structure lightweight/flexible) while strictly ensuring that the local Von Mises stress does not exceed the material's yield limit, overcoming the limitations of traditional approaches based solely on compliance minimization (e.g., Optimality Criteria).

## 🛠️ Technology Stack
* **Core Language:** Python 3.x
* **FEM Analysis:** Abaqus/CAE (Python Scripting & Abaqus Command Line)
* **Mathematical Optimization:** Method of Moving Asymptotes (MMA)
* **Key Libraries:** NumPy, SciPy, Math

## ⚙️ System Architecture
The framework is built on a robust iterative loop bridging the mathematical computing environment and the FEM solver:
1. **Initialization:** Mesh generation and initial density assignment ("Grey material").
2. **Automated FEM Analysis:** Background batch execution of Abaqus to extract stiffness matrices, displacements, and element stresses.
3. **Sensitivity Analysis:** Calculation of the objective function and constraint gradients with respect to the design variables (element densities).
4. **Topological Update:** Utilizing the MMA algorithm to determine the new material distribution, applying a strict *move-limit* to ensure numerical stability.
5. **Convergence:** Evaluation of the maximum density variation over the latest iterations.

## 🧠 Technical Challenges & Solutions
Stress-driven optimization is inherently a numerically unstable and ill-conditioned problem. During development, I successfully addressed several advanced critical issues:

* **P-Norm Aggregation Handling:** To avoid the computational burden of thousands of local constraints (one per element), stresses were aggregated into a single global measure using the P-Norm approach.
* **Resolving the "Singularity Phenomenon":** Managed numerical instabilities (e.g., `ZeroDivisionError` in the FEM solver) caused by low-density elements exhibiting artificially high stresses by appropriately tuning minimum densities and penalization factors.
* **Gradient Scaling (Ill-Conditioning):** Balanced the magnitude discrepancy between volume gradients (high) and stress gradients (low) by applying dynamic scaling factors. This allowed the MMA algorithm to correctly evaluate the Lagrange multipliers (Lambda) associated with stress, ensuring strict constraint satisfaction.
* **MMA Algorithm Tuning:** Optimized the asymptote parameters ($L_j$, $U_j$) and reduced the *move-limit* to prevent oscillations (checkerboard effect) and divergence during the early stages of the simulation.

## 📊 Results (Summary)
The framework is capable of processing complex 3D mechanical components, resulting in:
* Efficient material removal in load-neutral zones.
* Density redistribution to mitigate local stress peaks.
* Stable convergence without FEM solver failures.

---
*Project developed as an Engineering Degree Thesis.* 📫 **Contact:** [Insert your LinkedIn link here]
