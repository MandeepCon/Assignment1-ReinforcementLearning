# CSCN8020 — Assignment 1 

**Reinforcement Learning: Value Iteration vs. Off-Policy Monte Carlo**

This repository contains my solutions for **Assignment 1 (CSCN8020: Reinforcement Learning Programming)**.  
The assignment explores reinforcement learning algorithms applied to a **5×5 Gridworld** environment with goal and penalty states.

---

## Files

- **Assignment1-Mandeep.ipynb** → Jupyter Notebook with complete code, outputs, documentation, and analysis.  
- **README.md** → This documentation file.  
- **requirements.txt** → Environment dependencies (can be generated with `pip freeze`).   

---

## Problem Breakdown

### **Problem 1: Pick-and-Place Robot as an MDP**

### **Problem 2: Value Iteration in a 2×2 Gridworld**

### **Problem 3: Value Iteration**
- Implements **synchronous and in-place Value Iteration**.
- Environment: **5×5 Gridworld**, terminal goal at (4,4), grey penalty states `(0,4), (1,2), (3,0)`.
- Prints:
  - Value function tables (rounded).
  - Optimal greedy policy with arrows (**→, ←, ↑, ↓**) and symbols (**G = goal, X = grey**).
- Validates **convergence of VI** to the same optimal solution across both methods.

---

### **Problem 4: Off-Policy Monte Carlo (Weighted Importance Sampling)**
- Uses **Weighted Importance Sampling (WIS)** for off-policy MC control.
- Behavior policy: **uniform random (b)**.  
- Target policy: **greedy w.r.t. Q (π)**.  
- Learns **Q(s,a)** and greedy policy π from 20,000 sampled episodes.
- Produces:
  - Value function table from MC.
  - Greedy policy grid.
  - Comparison vs. VI baseline:
    - **MAE(|V* – V_MC|) ≈ 0.0184**
    - **Max Error ≈ 0.0440**
    - **MC runtime ≈ 1.464 s** vs. **VI runtime ≈ 0.0007 s**
    - VI converged in ~9 sweeps.

---

## Key Comparison

| **Aspect**               | **Value Iteration (VI)**                 | **Monte Carlo (MC with WIS)**             | **Observation**                          |
|--------------------------|------------------------------------------|--------------------------------------------|-------------------------------------------|
| **Method Type**          | Model-based (requires transition model) | Model-free (sampled episodes)              | VI needs model knowledge; MC works without |
| **Convergence & Accuracy** | Fast, precise, MAE ≈ 0.012              | Approximate, MAE ≈ 0.0184 (20k episodes)   | MC slower but closely matches VI           |
| **Computation Time**     | Very fast (~0.0007 s, ~9 sweeps)         | Slower (~1.464 s for 20k episodes)         | VI is much faster in small MDPs           |
| **Iterations/Episodes**  | ~9 sweeps                               | 20,000 episodes                            | MC needs many samples to reduce variance   |
| **Policy Quality**       | Optimal greedy policy                   | Greedy policy ≈ VI’s                       | Both consistent on this task               |
| **Notes**                | Deterministic, stable                   | Stochastic, higher variance                | Classic trade-off: model vs. data          |

---

## ⚙️ Environment Setup

1. **Create a virtual environment**

```bash
python -m venv .venv
# On Linux/Mac
source .venv/bin/activate
# On Windows
.venv\Scripts\activate
```

2. **Install dependencies**

```bash
pip install -U pip
pip install numpy matplotlib jupyter ipykernel
```

3. **Run the notebook**

```bash
jupyter notebook Assignment1-Mandeep.ipynb
```

---

## Dependencies

Minimal required packages:
```
numpy
matplotlib
jupyter
ipykernel
```

To capture the full environment (for submission or reproducibility), generate a `requirements.txt`:

```bash
pip freeze > requirements.txt
```

Install later with:
```bash
pip install -r requirements.txt
```

---

## Notes

- All results assume **reward-on-entry** convention.  
- Goal (G) is absorbing with **+10 reward**.  
- Grey states (X) impose **–5 penalty**.  
- Standard step cost is **–1**.  
- Discount factor: **γ = 0.9**.  

---

## 👤 Created
**Mandeep Singh Brar**  
CSCN8020 — Reinforcement Learning Programming  
Conestoga College  
