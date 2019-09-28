# homework 2

Name: Yifan Zhang

University ID: yz113

---

[TOC]

## Problem 1

> 1. In Interval Scheduling problem, if each request not only has a starting time and a finishing time but also has weight, and we want to maximize the total weights of intervals we selected. Can we still use the greedy algorithm that we learned during the lecture (process according to the finishing time)? If yes give a proof; if no give an counterexample.
> 2. Give a counter example showing that Dijkstra's algorithm does not work for graphs with negative edges. Please simulate the running of Dijkstra's algorithm on your counter example and explain why Dijkstra's algorithm fails in this case.

1. the answer is no. Here is a counterexample:

   ```mermaid
   gantt
       title Interval Scheduling
       dateFormat  mm
       axisFormat  %H:%M
       section Section
       task A1-weight 1          :a1, 00, 10m
       task A2-weight 100		 :a2, 05, 10m
       task A3-weight 2		 :a3, after a1, 4m
   ```

   If we still using a greedy algorithm that process according to the finishing time, task A1 and task A2 will be execute and task A3 will be dropped. However A3's weight is much more than A1's weight plus A2's weight.

2. This is the counter example showing that Dijkstra's algorithm does not work for graphs with negative edges:

   ```mermaid
   graph LR
   	subgraph S
       s[s, ds=0] -->|4| u[u, du=4]
       s -->|3| p[p, dp=3]
       end
       u -->|3| v[v]
       p -->|1| t[t]
       v-->|-7| t
   ```

   In next step, the algorithm will add node t in to S and define d(t) = 4, because d(t) = l(p, t) + d(p) = 4.

   However this is wrong, because if we go from s-->u-->v-->t, we will have a smaller d(t) = 0. As a result, Dijkstra's algorithm does not work for graphs with negative edges.

## Problem 2

>During the lecture, we learned a greedy algorithm to solve the Scheduling All Intervals problem. We also learned that a naive implementation of the greedy algorithm would take O(n^2) time. Please describe a more efficient implementation of the greedy algorithm with O(n log n) running time?

First, our algorithm sorts the intervals according to the start times. 

Then we can use a min heap to manage the end time of the interval running on each processor. At every time when we need to launch a new interval(in the order of the intervals start time), we check the root node of our min heap for the earliest idle processor. If the earliest intervals end time recorded in root node is later than the incoming interval, we will assigns the interval to a newly added processor, and add a new node to our min-heap to record the newly added processor's idle time. It will take $O(log~n~)$ to insert a node to the min heap. If the earliest interval end time is earlier than the incoming interval's start time, we will use this processor and update this min-heap node's value(the root node) to the new interval's end time and sort our min heap. It will take $O(log~n~)$ to sort a changed root node in min heap.

Our new algorithm will need $O(log~n~)$ on every step, and there are n steps. Overall, its running time is $O(nlog~n~)$.

## Problem 3

> On Thanksgiving day, you arrive on an island with n turkeys. You've already had thanksgiving dinner, so you don't want to eat the turkeys, but you do want to wish them all a Happy Thanksgiving.
> However, the turkeys each have very different sleep schedules. Turkey i is awake only in a single closed interval $[a_{i}, b_{i}]$. Your plan is to stand in the center of the island and say loudly "Happy Thanksgiving!" at certain times $t_{1},... ,t_{m}$. Any turkey who is awake at one of the times $t_{j}$ will hear the message. It's okay if a turkey hears the message more than once, but you want to be sure that every turkey hears the message at least once.
> Design a greedy algorithm which takes as input the list of intervals $[a_{i}, b_{i}]$ and outputs a list of times $t_{1},..., t_{m}$ so that $m$ is as small as possible and so that every turkey hears the message at least once. Your algorithm should run in time $O(n log~n~)$. Prove that your algorithm is correct.

- Algorithm description

  1. Sort every turkey's wake up time as a list $l$. It takes $O(nlog~n~)$.
  2. Use a min heap $h$ to manage turkey's sleep time.
  3. Pick up the earliest wake up turkey $e$ in $l$, if turkey $e$'s wake up time is later than the earliest sleep time $t$ marked in the root node of min heap $h$, schedule a "Happy Thanksgiving!" at time $t$, and free the min heap. This will take $O(1)$. Else, add $l$'s sleep time in to the min heap $h$. It takes $O(log~n~)$ to sort the min heap.
  4. If the list $l$ is not empty, go back to step 3.

  Over all, this algorithm's time complexity is $O(nlog~n~)$.

- Correctness proof