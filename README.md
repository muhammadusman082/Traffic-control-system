# Fuzzy Logic-Based Smart Traffic Signal Control System

A Python simulation of a smart, multi-lane traffic intersection that dynamically computes green-light durations using **Fuzzy Logic**, routes emergency vehicles through a road network using **informed search**, and detects/predicts congestion using **Machine Learning** — combined in a single object-oriented framework.

> **Course:** Artificial Intelligence Lab — Final Project, Iqra University
> **Author:** M Usman (Reg. No. 66985)

---

## Overview

Traditional traffic signals run on fixed timers and can't react to real conditions. This project models one intersection where:
- each lane's green-light duration adapts to live traffic (queue length + waiting time) via fuzzy reasoning,
- an emergency vehicle's fastest route is computed and instantly recalculated if the road network changes, and
- historical traffic data is mined for recurring congestion patterns and used to predict congestion risk.

## Features

- [x] **OOP design** — `TrafficIntersection`, `FuzzySignalController`, `EmergencyVehicleAgent`
- [x] **Fuzzy Logic control** — fuzzification (Low/Medium/High), a 9-rule Mamdani rule base, Centroid defuzzification
- [x] **Informed search** — BFS (baseline) vs. A* Search (Manhattan-distance heuristic) for emergency routing
- [x] **Dynamic Emergency Override** — a live obstacle forces an immediate route recalculation
- [x] **Unsupervised learning** — K-Means (K=3) clustering of congestion patterns
- [x] **Supervised learning** — MLPClassifier congestion-risk prediction with hyperparameter tuning

## Tech Stack

Python 3.x · NumPy · Matplotlib · scikit-learn (`KMeans`, `MLPClassifier`, `StandardScaler`) · scikit-fuzzy · Jupyter Notebook

## Installation

```bash
pip install numpy matplotlib scikit-learn scikit-fuzzy notebook
```

## Usage

```bash
jupyter notebook Traffic_Signal_System.ipynb
```

Then **Run All** (Cell → Run All, or Restart & Run All). No external dataset is needed — all historical traffic data is synthetically generated inside the notebook, so it runs standalone top to bottom.

## Project Structure

```
.
├── Traffic_Signal_System.ipynb   # full implementation, executed with outputs
└── README.md
```

## How It Works

1. **Fuzzy Signal Control** — `FuzzySignalController` fuzzifies Queue Length and Waiting Time into Low/Medium/High membership, evaluates the Mamdani rule base, and defuzzifies (Centroid) into a crisp green-light duration per lane.
2. **Emergency Routing** — `EmergencyVehicleAgent` searches a road-network grid from a dispatch point to the intersection with BFS and A*; A*'s admissible heuristic guarantees the shortest route while expanding fewer nodes.
3. **Dynamic Override** — a simulated live blockage near the agent's path forces A* to recalculate instantly, while the approaching lane gets temporary signal priority.
4. **Congestion Analytics** — K-Means groups synthetic (hour, volume) history into recurring congestion patterns; an MLPClassifier (tuned across a few hidden-layer sizes) predicts High/Low congestion risk from queue, wait, and hour.

## Sample Results

| Metric | Result |
|---|---|
| A* vs. BFS — 8×8 grid | 44 vs. 55 nodes expanded |
| A* vs. BFS — 14×14 grid | 115 vs. 172 nodes expanded |
| Emergency override | Route recalculated instantly after a live blockage |
| K-Means cluster sizes | 77 / 51 / 72 |
| Best MLPClassifier config | `(5,)` hidden units — 100% test accuracy |

## Status

✅ **Complete** — search, fuzzy logic, and both ML paradigms (unsupervised + supervised) are implemented, tested, and produce real, reproducible output.

## License

Academic project, shared for educational/coursework purposes.
