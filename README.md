# Transoms
A collection of good open-source projects on **TRANS**portation **O**ptimization, **M**odeling, and **S**imulation (**TRANSOMS**).

## Shortest Paths

1. [tntp](http://www.bgu.ac.il/~bargera/tntp/FW.zip) from Dr. Hillel Bar-Gera. One of the most efficient Deque implementations of the modified label correcting (MLC) algorithm in C. See mincostroutes.cpp for details. Its enhanced C++ counterpart can be found [here](https://github.com/jdlph/Path4GMNS/blob/master/engine/path_engine.cpp)
2. [jdlph/shortest-path-algorithms](https://github.com/jdlph/shortest-path-algorithms). A comprehensive list of the three special implementations of the MLC algorithm in Python including FIFO, Deque, and Dijkstra's algorithm. It also demonstrates how to boost their performances using proper data structures. Analysis on time complexity is provided. 
3. [nlperic/ta-lab](https://github.com/nlperic/ta-lab).  A simple [Python implementation](https://github.com/nlperic/ta-lab/blob/master/assignment/shortest_path.py) of the heap Dijkstra's algorithm and [Yen's algorithm](https://en.wikipedia.org/wiki/Yen%27s_algorithm) on solving the K-shortest paths problem (KSP) via a recursive call of the heap Dijkstra's algorithm. 

## Static User Equilibrium Traffic Assignment

The common approach to solve the static user equilibrium (UE) traffic assignment problem is [Frank-Wolfe (FW) algorithm](https://en.wikipedia.org/wiki/Frank%E2%80%93Wolfe_algorithm), which actually solves the linear approximation of the BMW model after the first-order Taylor approximation. 

Two of its core steps are finding a direction and then minimizing along this direction. The latter is essentially a linear search to determine the optimal step size (i.e., value of alpha), which can be obtained through methods using derivatives (e.g., Newton's method). However, numerical procedures without using derivatives are more common in transportation literature and applications due to their simplicity. Some examples include

1. Bisection method;
2. Golden section method;
3. 1 / i or 1 / (i + 1), where i is the current number of iteration.

They all lead to diminishing step sizes which will converge to zero. The diminishing step size is the cornerstone of convergency of traffic assignment. The third one is often referred to as the **method of successive averages (MSA)** in transportation literature. Note that **it is just a numerical procedure to compute step size** rather than an algorithm to solve the UE traffic assignment problem. In other words, any literature or application on traffic assignment claiming adopting MSA is still solving the problem using FW algorithm. There is **NO such MSA which could solely solve the traffic assignment problem**. 

As the BMW model features the arc-based or link-based formulation, it is sometimes called as **link-based UE**. UE can also be captured by variational inequality with respect to path flows, which often requires path enumeration (between each OD pair), and is thus referred to as **path-based UE**.

### Frank-Wolfe Algorithm

1. [AequilibraE](http://www.aequilibrae.com/python/latest/). It provides Conjugate FW (CFW) and Biconjugate FW (BFW) for faster convergency besides the standard implementation of FW algorithm. See [here](https://aequilibrae.com/python/V.0.6.1/traffic_assignment.html#algorithms-available) for details. It is also a comprehensive Python package for transportation modeling.
2. [chkwon/TrafficAssignment.jl](https://github.com/chkwon/TrafficAssignment.jl). A Julia package for finding traffic user equilibrium flow. Similar to AequilibraE, it also implements FW, CFW, and BFW along with golden section search method and Newton's method for line search.
3. [ZhengLi95/User-Equilibrium-Solution](https://github.com/ZhengLi95/User-Equilibrium-Solution). A standard implementation of FW algorithm with the Golden section method in Python with a detailed [writeup](https://github.com/ZhengLi95/User-Equilibrium-Solution/blob/master/static/user-equilibrium-solution.pdf).
4. [nlperic/ta-lab](https://github.com/nlperic/ta-lab). A simple implementation of FW algorithm with both the bisection method and MSA in Python only dependent on numpy.

### Gradient Projection

1. [asu-trans-ai-lab/DTALite](https://github.com/asu-trans-ai-lab/DTALite). A specialized gradient projection method to solve the variational inequality model for UE in C++. It is also an open-source AMS (Analysis, Modeling, and Simulation) library for efficiently macroscopic and mesoscopic traffic assignment, which has been widely used by U.S. Department of Transportation (DOT), state DOT's, local transportation agencies, etc. 
2. [jdlph/Path4GMNS](https://github.com/jdlph/Path4GMNS). An equivalent single-processing implementation in Python intended for both transportation planning and educational enrichment. It also provides a public API to the C++-based DTALite to conduct various multimodal traffic assignments.

## Dynamic Traffic Assignment

1. [asu-trans-ai-lab/DTALite](https://github.com/asu-trans-ai-lab/DTALite). Simulation-based dynamic traffic assignment (DTA) to manifest traffic evolution over time through some representation of traffic dynamics including kinematic wave model, spatial queue, etc.

## Traffic Simulation

Coming soon

## Vehicle Routing Problem

Coming soon
