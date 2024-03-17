### Techniques for Measuring Computational Cost
1. Speed timer
	 + simple 
	 + but slow and too dependent on compiler/machine
2. Count possible operations for an array of size N = 10,000:
	+ machine independent 
	+ but tedious to count
	+ 2B: count possible operations for an array of size N
		+ machine independent  + tells how algorithm scales
		+ even more tedious to compute + does not tell the actual time 
![[counting_exercise.png]]

**Comparing Algorithms:**
- Algo1 is better than algo2 because fewer operations to do the same work 
- better answer: algo1 **scales better** in the worst case
- even better answer: parabolas(N^2) grow faster than lines(N)

Algorithms which scale well (e.g. look like lines) have better asymptotic runtime behavior than algorithms that scale relatively poorly (e.g. look like parabolas).

We’ll informally refer to the “shape” of a runtime function as its                              order of growth (will formalize soon). 

### Simplifications: 
1. Consider only the worst case 
2. Pick some representative operation to act as a proxy for the overall runtime ("cost model")
	- a good choice is the operation with the largest number of counts
	- FROM PEYRIN LECTURE: Treat all operations as taking "1 unit of time". Increment as the same time as accessing array. 
3. Ignore lower order terms - only keep N^2 in (N^2 +N ) / 2 
4. Ignore multiplicative constants - remove / 2 

Geometric Reasoning: 
![[geometric reasoning.png]]

### Big-Theta
In “Big-Theta” notation we write this as R(N) ∈ Θ(f(N)).

![[big-theta.png]]

Using Big-Theta doesn't change anything about runtime analysis. No need to calculate k1 or k2. Just a formal version of "order of growth".

### Big O 
Whereas Big Theta can informally be thought of as something                                   like “equals”, Big O can be thought of as “less than or equal” and Big Omega can be thought of as "greater than or equal"

![[bigovsbigtheta.png]]

### Summary 
**Josh's approach:**
1. Choose a representative operation, and let C(N) be count of how many times that operation occurs as a function of N 
2. Determine order of growth f(N) for C(N) i.e. C(N) ∈ Θ(f(N))
	- Often (but not always) we consider the worst case count
3. If operation takes constant time, then R(N) ∈ Θ(f(N))
4. Can use O as an alternative for Θ. O is used for upper bounds. 

**Peyrin's approach**
1. Reduce constant time operations to "1 unit of time", and let C(N) be the count
of how many times that operation occurs as a function of N.
2. Determine order of growth f(N) for C(N), i.e. C(N) € Θ(f(N))
	- Often (but not always) we consider the worst case count.
3. Can use O as an alternative for Θ O is used for upper bounds. Ω isn't used
often in practical settings, but is often used in theoretical CS for lower
bounds.

### Big Omega
Big Omega can be thought of as "greater than of equal"
![[ocomparisons.png]]

**Uses for Big Omega:**
1. Very careful proofs of Big Theta runtime
2. Providing lower bounds for the hardness of a problem 

