# homework 5

Name: Yifan Zhang

University ID: yz113

---

[TOC]

## Problem 1

This is a P problem.

The given DNF Boolean formula is $DNF$.

```properties
for each clause in DNF:
	for each term in clause:
		if term conflicts with any other terms in this clause:
			then: jumpout this for loop
		else:
			if current term is the last term in this clause:
				return here is a truth assignment for X, such that DNF evaluates to be 1
```



## Problem 2

This is  a **NP-complete problem**.

1. Prove it is in **NP**

   The given graph $G=(V, E)$. Suppose the test solution is $S$.

   ``` properties
   k = 5
   for each node n in S:
   	remove every edge adjacent to v from set E
   	k = k - 1
   	if k >= 0 and E is empty:
   		then: S is a vertex cover in G
   	else: S is not a vertex cover in G
   ```

2. Prove it is in **NPC**

   > I have read note "16 Some Examples on Polynomial Reduction" when I solve this problem.

   We'll use a polynomial-time reduction from Independent Set to Vertex Cover.

   - Input reduction

     Given a graph $G=(V,E)$, independent set's parameter is $k$ and vertex cover's parameter is $k'=n-k$.

   - Proof of "equivalence"

     $\rightarrow$: Suppose that $S$ is an independent set in $G$. For any edge $e=(u,v) \in E$, we know that $u$ and $v$ will not be both in $S$. Namely, for any edge $e=(u,v)\in E$, either $u$ in $V-S$ or $v$ in $V-S$, which means that $V-S$ is a vertex cover.

     $\leftarrow$: Suppose that $V-S$ is an vertex cover in $G$. Suppose that there is an edge $e=(u,v) \in E$, and both $u$, $v$ are in $S$. Then there is a contradiction, because at least one of the nodes on either side of any edge should be in $V-S$. Only this way, $V-S$ will be a vertex cover. As a result, $V$ is a independent set.

## Problem 3

1. Prove it is in **NP**

   Suppose the test solution is $C$ and the length of $C$ is larger than $K$. The verification algorithm is very simple:

   ``` properties
   for each product in store:
   	for each customer in C:
   		if there are more than one customers in C buy this product:
   			return wrong soluion
   return true solution
   ```

2. Prove it is in **NPC**

   We'll use a polynomial-time reduction from Independent Set to this problem.

   - Input Reduction

     Given a graph $G=(V,E)$, each customer has a vertex. For each product, connect customers who have bought this product with each other in $G$. The parameter is $k$.

   - Proof of "equivalence"

     $\rightarrow$: Suppose that $S$ is an independent set in $G$. For any two vertexes $a, b$ in $S$, we know that there will not be an edge between $a$ and $b$, which means that for any two customers in $S$, they have not bought same products.

     $\leftarrow$: Suppose that $S$ is a solution of this problem. For any two customer  in $S$, we know that there will not be an edge between them, which means that this is an independent set.

## Problem 4

1. Prove it is **NP**

   Given a graph $G=(V,E)$. Suppose the test solution is $S$.

   ```properties
   for each node n in S:
   	for each node n' in V:
   		if e = (n, n') in E:
   			for each node n'' in S:
   				if e = (n', n'') in E:
   					return wrong solution
   return true solution
   ```

2. Prove it is in **NPC**

   For every edge $e = (u,v) \in E$, we can find a set $S_v \in V$ that for every $s_{vi}$ in $S_v$, there exist $e_i = (v, s_{vi}) \in E$. Then for every $s_{vi}$ in $S_v$, we'll add an edge $(u, S_{vi})$ to E. Finally we will have a new graph $G' = (V, E')$.
   
   Then apparently, when we try to find an independent set in $G'$, we are finding a strongly independent set in G.

## Problem 5

1. Prove it is **NP**

   Suppose the test solution is $S$.

   1. Check if $S$ contains more than $k$ jobs.
   2. Check if any two jobs in $S$ have a contradiction.

2. Prove it is in **NPC**

   We'll use a polynomial-time reduction from Independent Set to this problem.

   - Input Reduction

     Given a graph $G=(V,E)$, each jobs has a vertex. For each job, connect it to every other jobs in $G$ which has contradiction with this job. The parameter is $k$.

   - Proof of "equivalence"

     $\rightarrow$: Suppose that $S$ is an independent set in $G$. For any two vertexes $a, b$ in $S$, we know that there will not be an edge between $a$ and $b$, which means that for any two jobs in $S$, they will not have contradiction.

     $\leftarrow$: Suppose that $S$ is a solution of this problem. For any two jobs in $S$, we know that there will not be an edge between them, which means that this is an independent set.

## Problem 6

- Algorithm

  Given a graph $G=(V,E)$ and a black-box function $f(g)$, that $g$ is a graph as a parameter of $f$ and $f(g)$ return if there exist a Hamiltonian cycle in $g$. $|V| = m, |E| = n$

  ```properties
  G = (V, E)
  E' = E
  G' = (V, E')
  for each edge e in E:
  	// in this case, G' is a Hamiltonian cycle.
  	if |E'| == |V|:
  		then return G' = (V, E')
  		
  	// try to remove every edge and test if there still exist a Hamiltonian cycle.
  	G_test = (V, (E-e))
  	if f(G_test) == true:
  		then: remove e in E'
  	else: continue to next round
  ```

- Time complexity

  Suppose the black box function $f(g)$'s time complexity is x. Then the overall time complexity is $O(nx)$.

