# Private Multi-Agent LLM Optimization

Research project exploring the optimization of Privacy-Utility trade-offs in distributed Large Language Model (LLM) agent networks using nature-inspired metaheuristic search agents.

Collaborative research project under the guidance of **Professor Seyedali (Ali) Mirjalili** (Torrens University Australia).

---

## 1. Project Overview

Distributed multi-agent systems built on LLMs (e.g., using Google's Agent2Agent protocol or the Model Context Protocol) present unique privacy risks. Implementing Differential Privacy (DP) via local noise injection (Laplace/Gaussian mechanisms) bounds identity and membership leakage, but introduces a utility penalty. 

Currently, the privacy budget $\epsilon$ is set manually and uniformly across all agents, causing systems to either leak sensitive metadata or fail their collaborative tasks. This project formalizes this trade-off as a constrained optimization problem and evaluates nature-inspired metaheuristic algorithms to locate the optimal Pareto-frontier of agent-specific privacy budgets $\epsilon = (\epsilon_1, \epsilon_2, \dots, \epsilon_N)$.

### Mathematical Formulation

Given a network of $N$ LLM agents, our objective is to minimize the total adversarial membership-inference success rate $L(\epsilon)$ subject to task accuracy constraints:

$$\min_{\epsilon} L(\epsilon)$$

$$\text{subject to } U(\epsilon) \ge U_{\min}$$
$$\sum_{i=1}^N \epsilon_i \le \epsilon_{\text{budget}}$$
$$\epsilon_i \in [\epsilon_{\min}, \epsilon_{\max}]$$

Where:
* $L(\epsilon)$ is the empirical privacy leakage (measured via simulated membership inference attacks).
* $U(\epsilon)$ is the task completion accuracy of the collaborative multi-agent system.
* $\epsilon_{\text{budget}}$ is the total compliance cap (e.g., dictated by HIPAA or GDPR).

Since $L(\epsilon)$ and $U(\epsilon)$ are evaluated via stochastic simulation and black-box LLM calls, the objective landscape is non-convex and non-differentiable. We benchmark population-based metaheuristic solvers to navigate this space.

---

## 2. Solver Benchmarks

We compare classical optimization techniques against three nature-inspired algorithms developed by the CAIRO group:
1. **Grey Wolf Optimizer (GWO)**
2. **Whale Optimization Algorithm (WOA)**
3. **Salp Swarm Algorithm (SSA)**
4. **Particle Swarm Optimization (PSO)** (Baseline)

---

## 3. Directory Structure

```text
├── src/
│   ├── simulation/      # FastAPI & LangChain multi-agent testbed
│   │   ├── agents.py    # Agent definitions and behavior
│   │   └── protocol.py  # Agent-to-Agent (A2A) communications
│   ├── privacy/         # Differential Privacy interceptor layer
│   │   └── mechanisms.py# Laplace/Gaussian noise functions
│   └── optimization/    # Metaheuristic solvers (GWO, WOA, SSA, PSO)
│       └── solvers.py
├── notebooks/           # Pareto frontier analysis and plots
├── data/                # Synthetic datasets and evaluation logs
└── README.md
```

---

## 4. Weekly Progress Log

This log is updated weekly to track project milestones asynchronously.

| Week | Phase | Focus Area | Status | Deliverables / Notes |
| :--- | :--- | :--- | :--- | :--- |
| **Weeks 1-3** | Setup | DP-A2A Baseline Reproduction | ⏳ *Planned* | Porting Oulu prototype & validating initial baseline. |
| **Weeks 4-6** | Development | Multi-Agent Testbed & Interceptor | ⏳ *Planned* | FastAPI framework & DP client layer. |
| **Weeks 7-10**| Optimization | Metaheuristic Solvers Integration | ⏳ *Planned* | Solver runs and Pareto frontier generation. |
| **Weeks 11-13**| Expansion | Field-Specific Sensitivity | ⏳ *Planned* | Matrix budget allocation ($E \in \mathbb{R}^{N \times F}$). |
| **Weeks 14-16**| Submission | Manuscript Drafting & Release | ⏳ *Planned* | target submission for IEEE TETC / AAMAS 2027. |

---

## 5. Setup & Installation

*Instructions to run the simulation testbed locally will be added upon baseline initialization.*

```bash
# Clone the repository
git clone https://github.com/Ajayendra2705/private-multi-agent-llm.git
cd private-multi-agent-llm

# Initialize virtual environment
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r requirements.txt
```
