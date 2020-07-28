## Problem NP = P

### TL;TR;

P problem = easy to solve, easy to verify the solution, polynomial-time complexity  
NP problem = hard to solve, easy to verify  the solution, exponential-time complexity

If we can prove N = NP then for every actual NP problem, there exists a time-polynomial complexity algorithm to solve it.  
If we can prove N != NP then some algorithms cannot be solved by using a polynomial-time algorithm

Algorithm complexity : algorithm's operation quantity to solve the problem  

Class P  : low algorithm complexity | easy to verify the solution  
Class NP : high algorithm complexity | easy to verify the solution  

### 1 Solving and Verification

| item quantity | Operation Quantity to find the minimum | Operation quantity to sort list |
|:--------------|:---------------------------------------|:--------------------------------|
| 10            | 10                                     | 50                              |
| 100           | 100                                    | 5000                            |
| 1000          | 1000                                   | 500 000                         |

Complexity:
- to find the minimum : N operations  
- to sort the list : N<sup>2</sup>/2

Actually, the best sorting algorithm complexity : N ln(N)  

#### 1.1 Quick sort

| item quantity | Operation quantity |
|:--------------|:-------------------|
| 10            | 30                 |
| 100           | 600                |
| 1000          | 10000              |



#### 1.2 Sorting a list

_It is easier to verify that a list is sorted than to sort a list._  
=> if we detect that two items are not sorted, so we stop the verification.  
=> The maximal operation quantity to verify that a list is sorted : N Operations.  

With algorithms, we must find the solution and verify the solution.  

E.g, to find a solution to a Sudoku problem is harder to verify the solution.


#### 1.3 Knapsack problem

_Given a set of items, each with a weight and a value, determine the number of each item to include in a collection so that the total weight is less than or equal to a given limit and the total value is as large as possible_

[Knapsack problem](https://en.wikipedia.org/wiki/Knapsack_problem)

To solve, we can use the brut force, but there are 2<sup>N</sup>  

10 objects : 1024 combinations 
20 objects : about 1 million combinations  
60 objects :  10<sup>18</sup>
300 objects :  more combinations than atoms in the global universe

Exponential complexity : 2<sup>N</sup>  

But the solution verification is easy !  

- Find a solution : exponential complexity  
- Verify the solution : linear complexity  

#### 1.4 Prime factorization  

We want to decompose a number by using multiplication with only prime numbers.  

Example:  
- 30 = 3 x 2 x5  
- 10241 = 7 x 7 x 11 x 19  
- 56475871 = 7247 x 7793  

We use this kind of factorization for the RSA cryptosystem.

The complexity to decompose a number with N figures : _O_(10<sup>N</sup>).

The verification is easier than to solve the problem.  

### 2. Algorithm complexity Classes

#### 2.1 Class P 

=> This class contains all the polynomial problem => The polynomial problem complexity : _O(_N<sup>k</sup>_)_ with k=1,2... or N.log(N).  
The P-class problems are polynomial-time algorithm.  

#### 2.2 Exponential-time algorithm  

In this class, there is a subset in which the problems are hard to solve but easy to verify => those problems define _NP class_.  

NP stands for Non-determnistic Polymonial.  

#### 2.3 Class NP

NP problem => hard to solve but easy to verify a solution.

#### 2.4 Classes P and NP

NP problem => hard to solve and easy to verify  
P problem => easy to solve then easy to verify ==> So class NP also contains all P problems.  

NP problem set = {(P problem : easy to solve, easy to verify), (hard to solve, easy to verify)}

#### 2.5 The problem categorization evolution  

Some problems could switch from a category to another if the scientific community finds a new way to solve them.  
For example, the algorihm determining that a number is a prime number was an exponential-time problem before 2002. In 2002, three mathematicians (Agrawal, Kayal & Sanexa) propose a new algorithm with a polynomial-time complexity : _O(_N<sup>12<sup>_)_. And few years after, the complexity decrease up to _O(_N<sup>6<sup>_)_. This problem migrates to the P-problem class.

So we may ask this question regarding the willness to reduce the complexity of the NP-algorithm in order to find new algorithm with polynomial time complexity : _do it exist some NP problems for which it is impossible to find a polynomial-time algorithm ?_  
=> If yes, so the NP-class is different from the P-class.  

Else if all NP problem can be solved by using a polynomial algorithm, it means that if a problem solution can be verified in polynomial-time therefore this problem can also be also in polynomial-time => _Easy to verify then easy to solve_.   

#### 2.6 The question N=NP  

The question N=NP means P and NP are the same class.  

One way to demonstrate that the proposition is false (so in this case, the NP problems are different from the P problems) is to find only one algorithm with complexity lower-bounder equal to a complex-time.

### 3. Universal NP problem : SAT problem.

#### 3.1 The SAT problem

A SAT problem is boolean-logic problem. We define the problem by using logic constraints. 


#### 3.2 SAT problem equivalence

There exists the universal NP problem : the SAT problem.   
And the mathematicans demonstrated during the 70's the equivalence between the NP problem and SAT problem. Every NP problem has its equivalent SAT problem.  
If we know how to solve a SAT problem with a ploynomial-time algorithm, then we could to solve every NP problem with a polynomial-time algorithm.  

A SAT problem is  NP-complet.

### 4 Demonstration

=> if we want to prove that NP are different from P, then we have to find only one algorithm for which the complexity lower bound is greater than _O(_N log(N)_)_  
=> if we want to prove N = NP, then we have to find a NP-complet problem with a polynomial-time complexity.












