---
title: Heuristic Algorithm(启发式算法)
tags: Artificial Intelligence
categories: Artificial Intelligence
abbrlink: f7ee5063
date: 2020-03-10 17:13:01
---
# Heuristic Algorithm(启发式算法)
## general concept
a heuristic is a technique designed for solving a problem more quickly when classic methods are too slow, or for finding an approximate solution when classic methods fail to find any exact solution. This is achieved by trading optimality, completeness, accuracy, or precision for speed. In a way, it can be considered a shortcut.

<!-- more -->
## Travelling salesman problem(TSP)
> Given a list of cities and the distances between each pair of cities, what is the shortest possible route that visits each city and returns to the origin city?

TSP is known to be NP-Hard so an optimal solution for even a moderate size problem is difficult to solve. Instead, the greedy algorithm can be used to give a good but not optimal solution (it is an approximation to the optimal answer) in a reasonably short amount of time. The greedy algorithm heuristic says to pick whatever is currently the best next step regardless of whether that prevents (or even makes impossible) good steps later. It is a heuristic in that practice says it is a good enough solution, theory says there are better solutions (and even can tell how much better in some cases).

## Search
Another example of heuristic making an algorithm faster occurs in certain search problems. Initially, the heuristic tries every possibility at each step, like the full-space search algorithm. But it can stop the search at any time if the current possibility is already worse than the best solution already found. In such search problems, a heuristic can be used to try good choices first so that bad paths can be eliminated early (see alpha-beta pruning). In the case of best-first search algorithms, such as A* search, the heuristic improves the algorithm's convergence while maintaining its correctness as long as the heuristic is admissible.

## Antivirus software
Antivirus software often uses heuristic rules for detecting viruses and other forms of malware. Heuristic scanning looks for code and/or behavioral patterns common to a class or family of viruses, with different sets of rules for different viruses. If a file or executing process is found to contain matching code patterns and/or to be performing that set of activities, then the scanner infers that the file is infected. The most advanced part of behavior-based heuristic scanning is that it can work against highly randomized self-modifying/mutating (polymorphic) viruses that cannot be reliably detected by simpler string scanning methods. Heuristic scanning has the potential to detect future viruses without requiring the virus to be first detected somewhere else, submitted to the virus scanner developer, analyzed, and a detection update for the scanner provided to the scanner's users.

## 启发式算法
一个基于直观或经验构造的算法，在可接受的花费（指计算时间和空间）下给出待解决组合优化问题每一个实例的一个可行解，该可行解与最优解的偏离程度一般不能被预计。现阶段，启发式算法以仿自然体算法为主，主要有蚁群算法、模拟退火法、神经网络等。

# P-Problem vs NP-Problem
## 时间复杂度
- 时间复杂度则表示这个算法运行得到想要的解所需的计算工作量，他探讨的是当输入值接近无穷时，算法所需工作量的变化快慢程度。
## P-Problem(polynomial)
- A problem is assigned to the P (polynomial time) class if there exists at least one algorithm to solve that problem, such that the number of steps of the algorithm is bounded by a polynomial in n, where n is the length of the input.
- 算法的步数可以用多项式来表示
- P类问题：如果一个问题可以找到一个能在多项式的时间里解决它的算法

## NP-Problem(non-deterministic polynomial time)不确定性多项式时间
- A problem is assigned to the NP (nondeterministic polynomial time) class if it is solvable in polynomial time by a nondeterministic Turing machine.
-
- A P-problem (whose solution time is bounded by a polynomial) is always also NP. If a problem is known to be NP, and a solution to the problem is somehow known, then demonstrating the correctness of the solution can always be reduced to a single P (polynomial time) verification. If P and NP are not equivalent, then the solution of NP-problems requires (in the worst case) an exhaustive search.
-
- NP问题：可以在多项式的时间里验证一个解的问题/可以在多项式的时间里猜出一个解的问题
- 所有的P类问题都是NP问题。
- 不知道这个问题是不是存在多项式时间内的算法，所以叫non-deterministic不确定性，但是我们可以在多项式时间内验证并得出这个问题的一个正确解。

## NPC problem(non-deterministic polynomial complete)
- 如果所有NP问题都能在多项式时间内转化为最难的一个NP类问题（被约化成的问题应具有比前一个问题更复杂的时间复杂度），则称该NP问题为NPC问题

## NP-hard Problem
- A problem is said to be NP-hard if an algorithm for solving it can be translated into one for solving any other NP-problem. It is much easier to show that a problem is NP than to show that it is NP-hard. A problem which is both NP and NP-hard is called an NP-complete problem.

- 我们又叫NP难问题，他不是一个NP问题，然后所有的NPC问题都可以在多项式时间内转化为他的话，我们就叫他NPH（hard）问题。


Reference:
1. [wikipedia](https://en.wikipedia.org/wiki/Heuristic_(computer_science))
2. [mathworld](https://mathworld.wolfram.com/NP-Problem.html)
3. [matrix67.com](http://www.matrix67.com/blog/archives/105)
4. [blog.csdn](https://blog.csdn.net/databatman/article/details/49304295)
