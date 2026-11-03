# Lab 07: Implementation of Bayesian Network in Python

**Course:** AIC 301 — Machine Learning Lab  
**University:** Bahria University, Islamabad Campus  

---

## 📌 Lab Overview
This lab covers the theoretical foundation, modeling, and practical implementation of **Bayesian Networks** in Python using the `pgmpy` library.

### Key Objectives Covered:
1. **Bayesian Network Fundamentals:** Directed Acyclic Graphs (DAGs), conditional independence, chain rule of probability.
2. **Tabular Conditional Probability Distributions (TabularCPD):** Setting valid cardinality and ensuring all columns sum to 1.0.
3. **Model Verification:** Checking consistency and ensuring acyclicity using `model.check_model()`.
4. **Exact Probabilistic Inference:** Answering probabilistic queries with the `VariableElimination` algorithm.
5. **Two Complete Implementations:**
   - **Part 1 (Demonstration Problem):** Judea Pearl's classic *Burglary / Earthquake Alarm Network*.
   - **Part 2 (Lab Task):** *Student Performance Network* with 5 variables (`Attendance`, `StudyTime`, `Health`, `SocialLife`, `Performance`).

---

## 📁 Repository Structure

```
Lab-07-Bayesian-Networks/
│
├── lab_07_bayesian_networks.ipynb     # Fully executed, self-contained Jupyter Notebook
├── README.md                          # Complete lab report and documentation
└── plots/
    ├── student_network_dag.png        # Directed Acyclic Graph architecture
    └── performance_scenarios_comparison.png # Comparison of inference queries
```

---

## 🔬 Student Performance Network Architecture

```
      [Health]              [SocialLife]
       /    \                    |
      v      \                   v
[Attendance]  \             [StudyTime]
      \        \               /
       \        \             /
        v        v           v
           [Performance]
```

### Key Dependencies & Rationale:
- **`Health` $\rightarrow$ `Attendance`:** Illness directly causes class absences.
- **`SocialLife` $\rightarrow$ `StudyTime`:** High social commitments reduce available study hours.
- **`Attendance` $\rightarrow$ `Performance`:** Attending lectures provides continuous learning and assignment feedback.
- **`StudyTime` $\rightarrow$ `Performance`:** Independent study reinforces understanding and exam mastery.
- **`Health` $\rightarrow$ `Performance`:** Physical and mental stamina are essential during evaluations.

---

## 📊 Probabilistic Inference Results

| Scenario | $P(\text{Performance}=\text{Poor})$ | $P(\text{Performance}=\text{Average})$ | $P(\text{Performance}=\text{Excellent})$ |
| :--- | :---: | :---: | :---: |
| **Baseline (No Evidence)** | 27.6% | 49.8% | 22.6% |
| **High StudyTime & Good Health** | **6.7%** 📉 | 37.8% | **55.5%** 🏆 |
| **Low StudyTime & Poor Health** | **73.0%** ⚠️ | 22.0% | **5.0%** 📉 |

### Diagnostic (Backwards) Reasoning:
- **Query:** Given $P(\text{Health} \mid \text{Performance} = \text{Poor})$
- **Result:** Probability of Poor Health increases from baseline **25.0% $\rightarrow$ 37.4%**, demonstrating abductive diagnosis from effect back to cause.
