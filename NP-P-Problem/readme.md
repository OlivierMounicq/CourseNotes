## Problem NP = P

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
60 objects :  
300 objects :  

Exponential complexity : 2<sup>N</sup>  

But the solution verification is easy !  

- Find a solution : exponential complexity  
- Verify the solution : linear complexity  

### Prime factorization  

We want to decompose a number by using multiplication with only prime numbers.  

Example:  
- 30 = 3 x 2 x5  
- 10241 = 7 x 7 x 11 x 19  
- 56475871 = 7247 x 7793  

We use this kind of factorization for the RSA cryptosystem.

The complexity to decompose a number with N figures : _O_(10<sup>N</sup>).


### 2. Algorithm complexity Classes



### Class P - Class NP









