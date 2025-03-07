
# Table of content
- [Dynamic Programming](#dynamic-programming)
- [Equal Sum Partition Problem](#equal-sum-partition-problem)
- [Trapping Rain Water Problem](#trapping-rain-water-problem)
- [Longest Common Subsequence Problem](#longest-common-subsequence-problem)
- [Egg Dropping Puzzle](#egg-dropping-puzzle)

- [Climbing Stairs](#climbing-stairs)

- [Min Cost Climbing Stairs](#min-cost-climbing-stairs)

- [Unique Paths](#unique-paths)

<!-- Table of content -->
# Dynamic Programming
  - [Recursive vs Dynamic Programming Approach](#recursive-vs-dynamic-programming-approach)
  - [Properties](#properties)
  - [Advantages](#advantages)
  - [Disadvantages](#disadvantage)
  - [Problems](#problems)

Dynamic Programming is mainly an optimization over simple recursion.
Wherever we see a recursive solution that has repeated calls for same inputs, we can optimize it using Dynamic Programming.
The basic idea is to simply store the results of  the subproblems, so that we do not have to compute it again and again them when needed later. 
This simple optimization reduces time complexities from exponential to polynomial. 


### Recursive vs Dynamic Programming Approach :

#### Recursive:
```
int fibo(n)
  if n<=1
    return n;
  else
    fibo(n-1) + fibo(n-2);
```


#### Dynamic Programming:
```
f[0]=0;
f[1]=1;

for i=2 to n
  f[i]=f[i-1]+f[i-2];

return f[n];
```

### Properties

- Overlapping Subproblems
- Optimal Substructure

### Advantages

- As it is a recursive programming technique, it reduces the line code.
- One of the major advantages of using dynamic programming is it speeds up the processing as we use previously calculated references.

### Disadvantage

- It takes a lot of memory to store the calculated result of every subproblem without ensuring if the stored value will be utilized or not.
- In DP, functions are called recursively. Stack memory keeps increasing.

### Problems
 ```
 Given an array and a sum. Find if there is a subsequence present in the array with the given sum or not.
 ```
 ```
 Solution Link: 
 ```
---

# Equal Sum Partition Problem

- [Problem Statement](#problem-statement)
    - [Examples](#examples)
- [Explanation](#explanation)
- [Complexity](#complexity)


# Problem Statement

Given an array you have to output true or false depending on whether the array can be divided into two subsets such that the sum of both the subsets is equal. 

        > Note this question is a variation of 01 Knapsack problem

## Examples
```
Input: arr[] = {1, 5, 11, 5}
Output: true 
The array can be partitioned as {1, 5, 5} and {11}

Input: arr[] = {1, 5, 3}
Output: false 
The array cannot be partitioned into equal sum sets.

```
# Explanation

- Consider you are given an array.

- Let's say the array is divided into two subsets P1 and P2 and sum of P1 is S1 and P2 is S2.

- Now the questions says that sum of both the subsets must be same i.e S1=S2=S.

- This means the sum of the original array should be S+S=2S (Even as the number is 2*Sum).
This implies that we can get two such subsets when the sum of the original given array is Even.

    - In example arr[]= {1,5,11,5}
    Sum of array is 1+5+11+5=22 which is even. 

    - In example arr[]= {1,5,3}
    Sum of array is 1+5+3=9 which is odd and an odd number can never be divided into two equal parts.

     > Here you have to divide the number as int so you cannot divide the number as 11.5 and 11.5

- So in the question we can first calculate the sum of the array and ***if(sum%2!=0)*** (i.e sum=odd) we can return false

 ``` C++
    int sum=0;
    for(int i=0;i<size;i++)
        sum=sum+arr[i];

    if(sum%2!=0)
         return false;

 ```

- Now if the sum is even then 
we need to find one subset whose sum is S/2 because if we can find one subset with sum =S/2 then there will always be another subset with sum=S/2 as the sum of whole array is S.

So we call the subsetSum function.

``` C++
    input:arr[i]
      int sum=0;
    for(int i=0;i<n;i++)
        sum+=arr[i];

    if(sum%2!=0)
         return false;

    else if (sum%2==0)
        return subsetSum(arr,sum/2,n);

```
- In subsetSum function the problem can be solved using dynamic programming when the sum of the elements is not too big. We can create a 2D array t[][] of size (n+1)*(sum/2 + 1). And we can construct the solution in a bottom-up manner such that every filled entry has the following property  
```
t[i][j] = true if a subset of {arr[0], arr[1], ..arr[j-1]} has sum equal to i, otherwise false

```

## Following diagram shows the values in the partition table.  

![This is dp table](https://media.geeksforgeeks.org/wp-content/uploads/dynamicprogramming.jpg)

# Complexity
```
Time Complexity: O(sum*n) 
Auxiliary Space: O(sum*n) 
```

# Minimum_insertion_form_palindrome

- [Problem Statement](#problem-statement)
    - [Examples](#examples)
- [Explanation](#explanation)
- [Complexity](#complexity)

# Problem Statement

Consider a string str and output the minimum number of characters that need to be inserted to make it a palindrome. 

> This question is a variation of LCS (Longest Common Subsequence) problem


## Examples
```
Input: abcd
Output: 3
Number of insertions required is 3 i.e. dcbabcd

Input: abcda
Output: 2
Number of insertions required is 2 i.e. adcbcda 

Input: abcde
Output: 4
Number of insertions required is 4 i.e. edcbabcde


```
# Explanation

- Consider a string str: aebcbda
- We know that to make this string a palindrome we need to add a 'd' and an 'e' i.e  adebcbeda
- Here it can be seen that we needed to add 2 alphabets to make it a palindrome
- To find these we need to first find the LPS (Longest palindromic subsequence)
- To find the LPS find the length of LCS of the input string and its reverse
- From the LPS we can see that the minimum number of insertions needed would be the length of the input string minus LPS.
```
Number of insertions = Length of string - Length of LPS
```
So the function findMinInsertionsLCS would be
``` C++
    string rev = "";
	rev = str;
	reverseStr(rev);
	return (n - lcs(str, rev, n, n));
```


# Complexity
```
Time complexity: O(N^2) 
Space complexity: O(N^2) 

```

# [Trapping Rain Water Problem](https://leetcode.com/problems/trapping-rain-water/)
### Problem-Statement

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

### Examples

Input: arr[]   = {2, 0, 2}
Output: 2

We can trap 2 units of water in the middle gap

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20200429012104/Untitled-Diagram711.png" width="300" />



Input: arr[]   = {3, 0, 2, 0, 4}
Output: 7

We can trap "3 units" of water between 3 and 2,
"1 unit" on top of bar 2 and "3 units" between 2 
and 4.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20200429012307/Untitled-Diagram811.png" width="300" />

### Explanation

An element of the array can store water if there are higher bars on the left and right. The amount of water to be stored in every element can be found out by finding the heights of bars on the left and right sides. The idea is to compute the amount of water that can be stored in every element of the array. 

- Algorithm(Pseudo Code): 

  - Create two arrays left and right of size n. create a variable max_ = INT_MIN.
  - Run one loop from start to end. In each iteration update max_ as max_ = max(max_, arr[i]) and also assign left[i] = max_
  - Update max_ = INT_MIN.
  - Run another loop from end to start. In each iteration update max_ as max_ = max(max_, arr[i]) and also assign right[i] = max_
  - Traverse the array from start to end.
  - The amount of water that will be stored in this column is min(a,b) – array[i],(where a = left[i] and b = right[i]) add this value to total     amount of water stored
  - Print the total amount of water stored.

- Space Optimization for the Solution: 

Instead of maintaining two arrays of size n for storing the left and a right max of each element, maintain two variables to store the maximum till that point. Since water trapped at any element = min(max_left, max_right) – arr[i]. Calculate water trapped on smaller elements out of A[lo] and A[hi] first and move the pointers till lo doesn’t cross hi.

### Complexity
```
Time Complexity : O(n)
Space Complexity : O(1)
```

# [Longest Common Subsequence Problem](https://www.programiz.com/dsa/longest-common-subsequence)

### Problem Statement

Given two sequences, find the length of longest subsequence present in both of them. A subsequence is a sequence that appears in the same relative order, but not necessarily contiguous.

### Example

Let S1 and S2 be the two strings. Then the longest common subsequence **LCS** is given as 
```
Eg 1. 
S1 = {A, C, G, A, T, A, B} 
S2 = {C, Z, A, X, T, B, Q, P, R}
LCS = {C, A, T, B}

Eg 2.
S1 = {B, C, D, A, A, C, D}
S2 = {A, C, D, B, A, C}
LCS = {C, D, A, C}
```

### Explanation
- Consider two strings S1 -> ABACC and S2 -> AABBC.
- Create a LCS table of dimension **(n+1 * m+1)** where **n** and **m** are the lengths of S1 and S2 respectively.
  
  ``` LCS[m][n] ```
- The first row and the first column of the LCS table are filled with zeros since there will be no common subsequence when we compare string S1 or S2 with an empty string.

  ```
  if (i = 0 or  j = 0)
    LCS[i][j] = 0 
  ```
- For the remaining cells : 

   - If the character corresponding to the current row and current column are matching, this implies that the current character can be added to the LCS found upto previous character of both strings. Update the LCS table by adding 1 to the diagonal cell of the current character cell.

      ``` LCS[i,j] := LCS[i-1,j-1] + 1 ```
   - If the character corresponding to the current row and current column do not match, this implies that the current character cannot be added to the LCS. So the LCS found upto current character will be same as the maximum LCS found upto previos character of either strings. Fill the current cell by taking the maximum of previous column and previous row element from the LCS table

      ``` LCS[i,j] := max(LCS[i,j-1], LCS[i-1,j]) ```
    
    <br />

    ![image](https://user-images.githubusercontent.com/59263190/159671926-ca8db497-b132-40d1-9c17-c1d1a41a2aa8.png)


- ### Algorithm
```cpp
function computeLCS (S1[1...m], S2[1...n])
    LCS = array(0..m, 0..n)
    for i := 0 -> m
      for j := 0 -> n
        if i == 0 or j == 0
          LCS[i][j] = 0
        else if S1[i] == S2[j]
          LCS[i,j] := LCS[i-1,j-1] + 1
        else
          LCS[i,j] := max(LCS[i,j-1], LCS[i-1,j])
    
    return LCS[m][n]
```

### Complexity
```
Time Complexity : O(m*n)
Space Complexity : O(m*n)
```

# EGG DROPPING PUZZLE


- [Problem Statement](#problem-statement-for-egg-dropping)
- [Examples-1](#example-1)
- [Examples-2](#example-2)
- [Explanation](#explanation-2)
- [Complexity](#complexity-analysis)

### Problem Statement For Egg Dropping
You are given N identical eggs and you have access to a K-floored building from 1 to K.

There exists a floor f where 0 <= f <= K such that any egg dropped at a floor higher than f will break, and any egg dropped at or below floor f will not break. There are few rules given below. 

An egg that survives a fall can be used again.
A broken egg must be discarded.
The effect of a fall is the same for all eggs.
If the egg doesn't break at a certain floor, it will not break at any floor below.
If the eggs breaks at a certain floor, it will break at any floor above.
Return the minimum number of moves that you need to determine with certainty what the value of f is.
For more description on this problem see [Link](https://en.wikipedia.org/wiki/Dynamic_programming#Egg_dropping_puzzle)

##### Example 1:
Input:
N = 1, K = 2
Output: 2
##### Explanation 1: 
1. Drop the egg from floor 1. If it 
   breaks, we know that f = 0.
2. Otherwise, drop the egg from floor 2.
   If it breaks, we know that f = 1.
3. If it does not break, then we know f = 2.
4. Hence, we need at minimum 2 moves to
   determine with certainty what the value of f is.

##### Example 2:

Input:
N = 2, K = 10
Output: 4

##### Explanation 2: 
Method : Dynamic Programming.  
The approach will be to make a table which will store the results of sub-problems so that to solve a sub-problem, it would only require a look-up from the table which will take constant time, which took exponential time with recursion.  
Formally for filling DP[i][j] state where 'i' is the number of eggs and 'j' is the number of floors:   
 
We have to traverse for each floor 'x' from '1' to 'j' and find minimum of:  
(1 + max( DP[i-1][j-1], DP[i][j-x] )).  
![dptable](https://user-images.githubusercontent.com/78564629/158542308-490d8143-4889-425f-9d60-7e6632b8808c.png)



#### 2 egg for 100-floor builing- Optimal Approach:
If the first egg breaks, we need to test the remaining floors one by one starting from the lowest until the remaining egg breaks. For example, if the first drop is on the 50th floor and the egg breaks, it will take 49 more drops from the 1st floor to the 49th floor to ensure the remaining egg does not break until we know the answer.  
If the first drop is on the 10th floor and it breaks, then it takes a total of 10 trials to know the answer in a worst case scenario, i.e. the egg starts to break on the 9th or the 10th floor. The trials will be: 10 → 1 → 2 → 3 → 4 → 5 → 6 → 7→ 8 → 9  
To utilize the number of trials used (10 trials), if the first drop is on the 10th floor and the egg does not break, the second drop should be on the 19th floor, i.e. if the egg breaks on the 19th floor, then you should drop the eggs in the following sequence: 10 → 19 → 11 → 12 → 13 → 14 → 15 → 16 → 17 → 18 (10 trials in total).  
With this utilization in mind, the ultimate sequence (if an egg never breaks) will be 10 → 19 (10 + 9) → 27 (10 + 9 + 8) → 34 (10 + 9 + 8 + 7) → 40 → 45 → 49 → 52 → 54 → 55, i.e. 10 trials can test up to 55 floors.  
Using the formula for triangle numbers, m trials can test for \frac{m(m+1)}{2} floors, i.e.  
13 trials can test 13 * 14 / 2 = 91 floors  
14 trials can test 14 * 15 / 2 = 105 floors  
Thus it takes 14 trials to test a 100-floor building.  

##### 2 Egg for 15 Floor
![File](https://user-images.githubusercontent.com/78564629/158540414-3b65cc6b-e598-4347-b20b-79bdf10af759.png)


## Complexity Analysis
**Time Complexity :** O(nk^2).  
Where 'n' is the number of eggs and 'k' is the number of floors, as we use a nested for loop 'k^2' times for each egg  
**Auxiliary Space :** O(nk).  
As a 2-D array of size 'n*k' is used for storing elements.



# [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

- [Problem Statement of Climbing Stairs](#problem-statement-of-climbing-stairs)

- [Examples of Climbing Stairs](#examples-of-climbing-stairs)

- [Explanation of Climbing Stairs](#explanation-of-climbing-stairs)

- [Code](https://github.com/Shweta2024/LearnCPP/blob/climbing_stairs/D-DynamicProgramming/ClimbingStairs.cpp)

- [Analysis](#analysis)

### Problem Statement of Climbing Stairs

You are climbing a staircase. It takes n steps to reach the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?


### Examples of Climbing Stairs

##### Example 1

       
Input: n = 2

          Output: 2

          Explanation: There are two ways to climb to the top.

          1) 1 step + 1 step

          2) 2 steps 

#### Example 2:

###### The below diagram shows the three different ways of Climbing the Stairs


![cs](https://user-images.githubusercontent.com/75883328/160851148-014f971e-43eb-4cb3-8323-e41561717835.png)

       
Input: n = 3

          Output: 3

          Explanation: There are three ways to climb to the top.

          1) 1 step + 1 step + 1 step

          2) 2 steps + 1 step
 
          3) 1 step + 2 steps

### Explanation of Climbing Stairs

-We have to return the total number of possible ways to reach the n-th step, provided that we can either take one step or two step.

-So at any given stair (say currentStair) we'll have two options :- 1)to make a jump of one step or 2)to make a jump of two steps, therefore we'll make two recursive calls one for oneJump & another for twoJump.

-if we make a jump of one we'll reach to currentStair+1 and if we make a jump of two then we'll reach currentStair+2.

-if we reach the target stair ,then return 1,because it is a vaild way to reach the target.

-if we have gone beyond the target step,then return 0, because we can't reach the target stair.


This recursive code will give us a TLE.So, we need to optimize this.

We'll optimize this using DP ,because we have overlapping sub-problems.

-So we can store the values in a hash map and will use those values from the hash map only instead of making recursive calls for it.

### Pseudo code

```
int totalWays(int currentIndex,int target,unordered_map<int,int>&m)

           if(currentIndex==target) return 1; 
	   
           if(currentIndex>target) return 0;
	   
	   int currentKey=currentIndex;
	   
	   if(m.count(currentKey)) return m[currentKey];
	   
	   int oneJump=totalWays(currentIndex+1,target,m);
	   
           int twoJump=totalWays(currentIndex+2,target,m);
	   
	   m[currentKey]=oneJump+twoJump;
        
    return m[currentKey];

```


### The below is the Screenshot of my output

###### Output for n=4

![op1](https://user-images.githubusercontent.com/75883328/160851883-c485d803-7892-4ced-b15f-edc00eb8491f.png)


###### Output for n=44

![op2](https://user-images.githubusercontent.com/75883328/160852013-dc76d8b2-8b29-4a00-8f7b-b82a21bd868f.png)



### Analysis
#### Time Complexity = O(n)


#### Space Complexity = O(n)


# [Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/)

- [Problem Statement of Min Cost Climbing Stairs](#problem-statement-of-min-cost-climbing-stairs)

- [Examples of Min Cost Climbing Stairs](#examples-of-min-cost-climbing-stairs)

- [Explanation of Min Cost Climbing Stairs](#explanation-of-min-cost-climbing-stairs)

- [Code Link](https://github.com/Shweta2024/LearnCPP/blob/Min_Cost_Climbing_Stairs/D-DynamicProgramming/MinCostClimbingStairs.cpp)

- [Time Complexity and Space Complexity](#time-complexity-and-space-complexity)
-  [Output](#output)


### Problem Statement of Min Cost Climbing Stairs

You are given an integer array cost where cost[i] is the cost of ith step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from the step with index 0, or the step with index 1.

Return the minimum cost to reach the top of the floor.


### Examples of Min Cost Climbing Stairs


![3](https://user-images.githubusercontent.com/75883328/161399647-bebbc27d-80b6-4c1a-a581-ba11518c7ea0.png)


##### Example 1

Input: cost = [10,15,20]

Output: 15

Explanation: You will start at index 1.
- Pay 15 and climb two steps to reach the top.
The total cost is 15.


#### Example 2:

Input: cost = [1,100,1,1,1,100,1,1,100,1]

Output: 6

Explanation: You will start at index 0.
- Pay 1 and climb two steps to reach index 2.
- Pay 1 and climb two steps to reach index 4.
- Pay 1 and climb two steps to reach index 6.
- Pay 1 and climb one step to reach index 7.
- Pay 1 and climb two steps to reach index 9.
- Pay 1 and climb one step to reach the top.
The total cost is 6.


### Explanation of Min Cost Climbing Stairs

- We have to Return the minimum cost to reach the top of the floor, provided that we can either take one step or two step and can either start from the step with index 0, or the step with index 1.

- So at any given stair (say currentStair) we'll have two options :- 1)to make a jump of one step or 2)to make a jump of two steps, therefore we'll make two recursive calls one for oneJump & another for twoJump and if we make a jump from the currentStair then we have to pay an amount i.e. cost[currentStair].

- if we make a jump of one we'll pay cost[currentStair] and will reach to currentStair+1 and if we make a jump of two then we'll reach currentStair+2 by paying the same amount.

- if we reach the target stair ,then return 0,because we don't need to pay any amount to reach the target stair from the target.

- if we have gone beyond the target step,then return infinity, because we can't reach the target stair.


This recursive code will give us a TLE.So, we need to optimize this.

We'll optimize this using DP ,because we have overlapping sub-problems.

- So we can store the values in a hash map and will use those values from the hash map only instead of making recursive calls for it.


### Pseudo code


```

          int minCost(vector<int>&cost,int currentIndex,unordered_map<int,int>&m)
                  if(currentIndex==cost.size()) return 0; 
                  if(currentIndex>cost.size()) return 999;
        
                  int currentKey=currentIndex;
        
                  if(m.count(currentKey)) return m[currentKey];
        
                  int oneJump= cost[currentIndex] + minCost(cost,currentIndex+1,m);
                  int twoJump= cost[currentIndex] + minCost(cost,currentIndex+2,m);
        
                  m[currentKey]= min(oneJump,twoJump);
        
                  return m[currentKey];
		  
```


 
### Output
### The below is the Screenshot of my output

###### Output for cost = [10,15,20]


![1](https://user-images.githubusercontent.com/75883328/161399432-35952f0e-9ea2-48f9-93f9-e2124d7a0b0f.png)



###### Output for cost = [1,100,1,1,1,100,1,1,100,1]

![2](https://user-images.githubusercontent.com/75883328/161399444-22dbea8a-9bda-4a36-96c1-0037079da70d.png)


### Time Complexity and Space Complexity

Time Complexity = O(n)

Space Complexity = O(n)


# [Unique Paths](https://leetcode.com/problems/unique-paths/)

- [Problem Statement of Unique Paths](#problem-statement-of-unique-paths)

- [Examples of Unique Paths](#examples-of-unique-paths)

- [Explanation of Unique Paths](#explanation-of-unique-paths)

- [Pseudo Code of Unique Paths](#pseudo-code-of-unique-paths)

- [Code Link](https://github.com/Shweta2024/LearnCPP/blob/UniquePaths/D-DynamicProgramming/UniquePaths.cpp)

- [Time Complexity and Space Complexity of Unique Paths](#time-complexity-and-space-complexity-of-unique-paths)

-  [Output of Unique Paths](#output-of-unique-paths)


### Problem Statement of Unique Paths

There is a robot on an m x n grid. The robot is initially located at the top-left corner (i.e., grid[0][0]). The robot tries to move to the bottom-right corner (i.e., 

grid[m - 1][n - 1]). The robot can only move either down or right at any point in time.

Given the two integers m and n, return the number of possible unique paths that the robot can take to reach the bottom-right corner.


### Examples of Unique Paths


##### Example 1:

![image](https://user-images.githubusercontent.com/75883328/161976152-6f2972ee-4561-4ffe-ac27-d27bd9ebe82b.png)


Input: m = 3, n = 7

Output: 28



##### Example 2:

Input: m = 3, n = 2

Output: 3

Explanation: From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:

1. Right -> Down -> Down

2. Down -> Down -> Right

3. Down -> Right -> Down


### Explanation of Unique Paths

- we have to return the number of possible unique paths that the robot can take to reach the bottom-right corner (i.e., grid[m - 1][n - 1]) from top-left corner (i.e., grid[0][0])

- So from any cell of the grid we are having 2 options :-  1.either move down or 2. move right at any point in time.

- if we'll move down we'll reach grid[i+1][j] and on moving right we'll reach gird[i][j+1].

- if we'll reach grid[m-1][n-1] then. return 1 because its a valid path.

- if at any point i<0 or j<0 then, return 0 because its an invalid path.


This recursive code will give us a TLE.So, we need to optimize this.

We'll optimize this using DP ,because we have overlapping sub-problems.

- So we can store the values in a vector and will use those values from the vector only instead of making recursive calls for it.


### Pseudo code of Unique Paths



    int totalPaths(int currentRow,int currentCol,int targetRow,int targetCol,vector<vector<int>>&v)
         if(currentRow==targetRow && currentCol==targetCol) return 1;
         if(currentRow<0 || currentCol<0 ||currentRow>targetRow ||currentCol>targetCol) return 0;
        
         if(v[currentRow][currentCol]!=-1) return v[currentRow][currentCol];
        
   
         int right = totalPaths(currentRow,currentCol+1,targetRow,targetCol,v); 
         int down = totalPaths(currentRow+1,currentCol,targetRow,targetCol,v); 
        
         v[currentRow][currentCol] = (right+down); 
         return v[currentRow][currentCol];
   



### Output of Unique Paths

###### Output for  m = 3, n = 7

![image](https://user-images.githubusercontent.com/75883328/161979235-37d30429-4f84-4533-88b8-8f82eff40fc8.png)


###### Output for m = 3, n = 2

![image](https://user-images.githubusercontent.com/75883328/161979330-a98223f7-4aff-411a-8ee4-dc099ea89768.png)


### Time Complexity and Space Complexity of Unique Paths

#### Time Complexity = O(m * n)


#### Space Complexity = O(m * n)
