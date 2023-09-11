# TAP101
A collection of good open-source projects covering the fundamental components related to the Traffic Assignment Problem (TAP).

## Shortest Paths

1. [tntp](http://www.bgu.ac.il/~bargera/tntp/FW.zip) from Dr. Hillel Bar-Gera. One of the most efficient Deque implementations of the modified label correcting (MLC) algorithm in C. See mincostroutes.cpp for details. Its enhanced C++ counterpart has been served as the path engine for [Path4GMNS](https://github.com/jdlph/Path4GMNS/blob/master/engine/path_engine.cpp) and [TransOMS](https://github.com/jdlph/TransOMS).
2. [jdlph/shortest-path-algorithms](https://github.com/jdlph/shortest-path-algorithms). A comprehensive list of the three special implementations of the MLC algorithm in Python including FIFO, Deque, and Dijkstra's algorithm. It also demonstrates how to boost their performances using proper data structures. Analysis on time complexity is provided.
3. [nlperic/ta-lab](https://github.com/nlperic/ta-lab).  A simple [Python implementation](https://github.com/nlperic/ta-lab/blob/master/assignment/shortest_path.py) of the heap Dijkstra's algorithm and [Yen's algorithm](https://en.wikipedia.org/wiki/Yen%27s_algorithm) on solving the K-shortest paths problem (KSP) via a recursive call of the heap Dijkstra's algorithm.

## Static User Equilibrium Traffic Assignment

The common approach to solve the static user equilibrium (UE) traffic assignment problem is [Frank-Wolfe (FW) algorithm](https://en.wikipedia.org/wiki/Frank%E2%80%93Wolfe_algorithm), which actually solves the linear approximation of the BMW model after the first-order Taylor approximation.

Two of its core steps are finding a direction and then minimizing the objective function along this direction. The latter is essentially a linear search to determine the optimal step size, which can be obtained through methods using derivatives. However, numerical procedures without using derivatives are more common in transportation literature and applications due to their simplicity. Some examples include

1. Bisection method;
2. Golden section method;
3. 1 / i or 1 / (i + 1), where i is the current number of iteration.

They all lead to diminishing step sizes which will converge to zero. The diminishing step size is the cornerstone of convergency of traffic assignment. The first two methods deal with the derivative of the objective function (i.e., they are methods using derivatives). The third one is often referred to as the **method of successive averages (MSA)** in transportation literature. Note that **it is just a numerical procedure to compute step size** rather than an algorithm to solve the UE traffic assignment problem. In other words, any literature or application on traffic assignment claiming adopting MSA is still solving the problem using FW algorithm. There is **NO such MSA which could solely solve the traffic assignment problem**.

As the BMW model features the arc-based or link-based formulation, it is sometimes called as **link-based UE**. UE can also be captured by variational inequality with respect to path flows, which often requires path enumeration (between each OD pair), and is thus referred to as **path-based UE**.

### Frank-Wolfe Algorithm

1. [AequilibraE](http://www.aequilibrae.com/python/latest/). It provides Conjugate FW (CFW) and Biconjugate FW (BFW) for faster convergency besides the standard implementation of FW algorithm. See [here](https://aequilibrae.com/python/V.0.6.1/traffic_assignment.html#algorithms-available) for details. It is also a comprehensive Python package for transportation modeling.
2. [chkwon/TrafficAssignment.jl](https://github.com/chkwon/TrafficAssignment.jl). A Julia package for finding traffic user equilibrium flow. Similar to AequilibraE, it also implements FW, CFW, and BFW along with golden section search method and Newton's method for line search.
3. [ZhengLi95/User-Equilibrium-Solution](https://github.com/ZhengLi95/User-Equilibrium-Solution). A standard implementation of FW algorithm with the Golden section method in Python with a detailed [writeup](https://github.com/ZhengLi95/User-Equilibrium-Solution/blob/master/static/user-equilibrium-solution.pdf).
4. [nlperic/ta-lab](https://github.com/nlperic/ta-lab). A simple implementation of FW algorithm with both the bisection method and MSA in Python only dependent on numpy.

### Gradient Projection

1. [DTALite](https://github.com/asu-trans-ai-lab/DTALite). A specialized gradient projection method to solve the variational inequality model for UE in C++. It is also an open-source AMS (Analysis, Modeling, and Simulation) library for efficiently macroscopic and mesoscopic traffic assignment, which has been widely used by U.S. Department of Transportation (DOT), state DOT's, local transportation agencies, etc.
2. [Path4GMNS](https://github.com/jdlph/Path4GMNS). An equivalent single-processing implementation in Python intended for both transportation planning and educational enrichment. It also provides a public API to the C++-based DTALite to conduct various multimodal traffic assignments.

## Dynamic Traffic Assignment

1. [DTALite](https://github.com/asu-trans-ai-lab/DTALite). Simulation-based dynamic traffic assignment (DTA) to manifest traffic evolution over time through some representation of traffic dynamics including kinematic wave model, spatial queue, etc.
2. [Path4GMNS](https://github.com/jdlph/Path4GMNS). A simple traffic simulator using the point queue model. The routing decisions could be from the UE traffic assignment or simply following the shortest paths.
3. [TransOMS](https://github.com/jdlph/TransOMS). It features a modern, cross-platform, and lightning-fast DTA system besides the same functionality as DTALite.

## Good References

1. Sheffi, Y. (1985). [Urban Transportation Networks: Equilibrium Analysis with Mathematical Programming Methods](http://web.mit.edu/sheffi/www/selectedMedia/sheffi_urban_trans_networks.pdf). Prentice-Hall.
2. Boyles, S. D., N. E. Lownes, & A. Unnikrishnan. (2023). [Transportation Network Analysis, Volume I, Version 0.91](https://sboyles.github.io/book.pdf).
3. Bertsekas, D., & Gafni, E. (1983). [Projected Newton methods and optimization of multicommodity flows](https://web.mit.edu/dimitrib/www/Gafni_Newton.pdf). IEEE Transactions on Automatic Control, 28(12), 1090–1096.
4. Jayakrishnan, R., Tsai, W. K., Prashker, J. N., & Rajadyaksha, S. (1994). [A Faster Path-Based Algorithm for Traffic Assignment (Working Paper UCTC No. 191)](https://escholarship.org/uc/item/2hf4541x). The University of California Transportation Center.
5. Peeta, S., & Ziliaskopoulos, A. K. (2001). Foundations of Dynamic Traffic Assignment: The Past, the Present and the Future. Networks and Spatial Economics 2001 1:3, 1(3), 233–265. https://doi.org/10.1023/A:1012827724856
6. Zhou, X., & Taylor, J. (2014). DTALite: A queue-based mesoscopic traffic simulator for fast model evaluation and calibration. Cogent Engineering, 1(1). https://doi.org/10.1080/23311916.2014.961345