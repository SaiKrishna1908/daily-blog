---
title: Dynamic Programming & Related Problems
date: '2020-07-10'
tags: ['competative programming', 'dynamic programming', 'algorithms']
draft: false
summary: Dynamic Programming in a nut shell
images: []
layout: PostLayout
canonicalUrl:
---

# Dynamic Programming Notes & Problems

##

## **Dynamic Programming With Memoization**

```
int dp_state[n]

void solve(int i) {
    # Base cases

    # Check if dp solution is already present
    if (dp_state[i] exists) {
        return dp_state[i];
    }
   
    # If not process the solution
    int sol = solve(i-1);
   
    dp_state[n] = sol;

    return sol;
}
```

## **Dynamic Programming Basics**

Each state in a DP will take a dimension in a array.

Before starting the problem, ask these questions :

1. How many states will be there in my dp ?
2. What does each state in my dp represent ?
3. How do we transition to new state, i.e how do we compute dp\[i\]  using previous values ?

For performing mod after updating dp

```
const int mod = 1e9+7;

dp[i] = dp[i-1] + dp[i-2];

// This is less costly than mod operation
if (dp[i] >= mod) {
    dp[i] = dp[i] - mod;
}
```

**Dynamic Programming Usage:**

- DP can be used along with Memoization to avoid already computed solutions to known problems.
- DP can be used to break a problem into sub problems and using their solutions to solve the original problem

**Top\-Down Approach:** In the top\-down approach, we implement the solution naturally using recursion but modify it to save the solution of each subproblem in an array or hash table. This approach will first check whether it has previously solved the subproblem. If yes, it returns the stored value and saves further calculations. Otherwise, top\-down approach will calculate sub\-problem solutions in the usual manner. We say it is the memoized version of a recursive solution, i.e., it remembers what results have been computed previously.
%\!\(EXTRA markdown.ResourceType=, string=, string=\)

**Bottom\-Up Approach:** In the top\-down approach, we implement the solution naturally using recursion but modify it to save the solution of each subproblem in an array or hash table. This approach will first check whether it has previously solved the subproblem. If yes, it returns the stored value and saves further calculations. Otherwise, top\-down approach will calculate sub\-problem solutions in the usual manner. We say it is the memoized version of a recursive solution, i.e., it remembers what results have been computed previously.

%\!\(EXTRA markdown.ResourceType=, string=, string=\)

```
coin-change: https://www.geeksforgeeks.org/understanding-the-coin-change-problem-with-dynamic-programming/
buckets: https://codeforces.com/problemset/problem/706/B

burst bubble: https://leetcode.com/problems/burst-balloons/
https://github.com/SaiKrishna1908/MyCPSolutions/blob/main/cp_solutions/burst_bubble.cpp

merge stones: https://leetcode.com/problems/minimum-cost-to-merge-stones/

Number of Dice Rolls: https://leetcode.com/problems/number-of-dice-rolls-with-target-sum/
```

## Finding max possible sum from contiguous elements using dp

```
void find_man_sum(int array[], int size) {
   
    int curr_max = array[0];
    int max_so_far = array[0];

    for(int i=1;i<size;i++) {
        curr_max = max(array[i], array[i] + curr_max);
        max_so_far = max(max_so_far, cur_max);
    }

    return max_so_far;
}
```

## Fibonacci Numbers

```
dp[n];

dp[0] = 0;
dp[1] = 0;

for(int i=2 .. n) {
    dp[i] = dp[i-1] + dp[i-2];
}

```

## Stairs Problem to learn dp

### _Problem Type 1_

You are climbing a staircase. It takes N steps to reach to the top. Each time you either climb 1 or 2 steps. In how many distant ways can you climb to the top ?

Ask yourself below questions when tackling dp problems

```
What are the states of dp ?
In this case, at i step we don't care how we got there, the only thing that matters is where we are. So we have a dp of state of 1.

What does each state of dp represent ?

dp[i] represent the number of ways to reach that step.

How do we transition to new state, i.e how do we compute dp[i]  using previous values ?

We can get to ith step either from i-1th step or i-2th step

therefore,

dp[i] = dp[i-1] + dp[i-2]

```

### _Problem Type 2_

You are climbing a staircase. It takes N steps to reach to the top. Each time you climb at most k steps. In how many distant ways can you climb to the top ?

```
What are the states of dp ?
In this case, we have to consider from which step we have landed on the present step as there are atmost k different ways we have come here. So we have 2 states in our dp

What does each state of dp represent ?
dp[i][j] represent the number of ways to reach that step.

How do we transition to new state, i.e how do we compute dp[i]  using previous values ?
We can get to ith step either from i-1th step or i-2th step
therefore, 

```

### _Problem Type 3_

### **_Combination Sum_**

Given the target value N and an array of allowed numbers, count ways to write N as sum of these numbers.

```
* What are the states of dp ?
 To answer this question, check what is important so far ? For example here we need to keep track of what is the sum so far. So, we only need 
1 state for our dp.
Note: Here we don't care how are numbers are made, we just care about sum until now.

* What does each state in dp represent ?
dp[i] represents the number of ways we can get sum i.

* How to transition to new state, i.e how do we compute dp[i] using previous values ?
dp[0] = 1
for i in 1...N :
	for x in num:
		dp[i] = dp[i] + dp[i-x]
dp[i-x] is used to get sum until i using a number x.
```

How does this work ?

```
initial stage = [1,0,0,0,0]
(i =1, x = 1) :  dp[1] = dp[1] + dp[1-1]
			dp[1] = dp[1] + dp[0]
[1,1,0,0,0]
(i=1, x=2):   dp[1] = dp[1] + dp[1-2]
[1,1,0,0,0]

(i=1,x=3):   dp[1] = dp[1] + dp[1-3]
[1,1,0,0,0]

(i=2,x=1):   dp[2] = dp[2] + dp[2-1]
[1,1,1,0,0]

(i=2,x=2): dp[2] = dp[2] + dp[2-2]
[1,1,2,0,0]

(i=2,x=3): dp[2] = dp[2] + dp[2-3]
[1,1,2,0,0]

(i=3, x=1): dp[3] = dp[3] + dp[3-1]
[1,1,2,2,0]

(i=3,x=2): dp[3] = dp[3] + dp[3-2]
[1,1,2,3,0]

(i=3,x=3): dp[3] = dp[3] + dp[3-3]
[1,1,2,4,0]
```

### _Knapsack DP without item repetition_

### Problem 1:

There are N items, numbered 1,2,…,N. For each i \(1≤i≤N\), Item i has a weight of wi and a value of

vi.

Taro has decided to choose some of the

N items and carry them home in a knapsack. The capacity of the knapsack is W, which means that the sum of the weights of items taken must be at most

W.

Find the maximum possible sum of the values of items that Taro takes home.

```
* What are the states of dp ?
 We keep track of the maximum value we can get for a weight i. So we need a dp of state 1.

* What does each state in dp represent ?
dp[i], represents the maximum value we can get for weight i.

* How to transition to new state, i.e how do we compute dp[i] using
previous values ?

int w // total weight of the knapsack

for (int i = 0; i < n; i++)
  {
    int weight, value;

    cin >> weight >> value;

   for(int j=w;j>=weight;j--) {
     dp[j] = max(dp[j], (j-weight >= 0 ? dp[j-weight] : 0) + value);
   }   
}
```

Transition with example

Input:

6 15  6 items, 15 total weight of knapsack

6 5

5 6

6 4

6 6

3 5

7 2

```
dp transition

0 0 0 0 0 0 5 5 5 5 5 5 5 5 5 5
0 0 0 0 0 6 6 6 6 6 6 11 11 11 11 11
0 0 0 0 0 6 6 6 6 6 6 11 11 11 11 11
0 0 0 0 0 6 6 6 6 6 6 12 12 12 12 12
0 0 0 5 5 6 6 6 11 11 11 12 12 12 17 17
0 0 0 5 5 6 6 6 11 11 11 12 12 12 17 17
```

### Problem 2:

Same as problem 1 but with different constrains

1≤N≤100

1≤W≤10^9

1≤wi≤W

1≤vi≤10^3

```
* What are the states of dp ?
We keep track of the minimum weight we can get for a value i. So we need a dp of state 1.

* What does each state in dp represent ?
dp[i], represents the minimum weight required to get value i.

* How to transition to new state, i.e how do we compute dp[i] using
previous values ?

vector<ll> dp(max_val+1);

  fill(dp.begin(), dp.end(), INF);

  dp[0] = 0;
  for(int i=0;i<n;i++) {           
      auto current_pair = input[i];     
      int current_value = current_pair.second;           
     
      for(int val = dp.size();val>=current_value;val--) {
              dp[val] = min(dp[val], input[i].first + dp[val-current_value]);
      }
   
  }
```

### _Largest  Common Subsequence:_

### Problem 1:

Given two strings s and t find the length of the largest common sequence occurring in the given strings.

ex:

s = abracadabra

t = avadakedavra

ans = aaadara

```
1. How many states will be there in my dp ?
** There will be 2 states

2. What does each state in my dp represent ?
** dp[i][j] represents the maximum subsequence possible with string s of length s[0..i] and
    string t of length t[0..j].

3. How do we transition to new state, i.e how do we compute dp[i]  using previous values ?
** The transition rules are as follows:
      if s[i] == t[j]
        the following statements says that dp[i][j]
        is equal to 1 + maximum subsequence in s[i-1] t[j-1]
        dp[i][j] = dp[i-1][j-1] + 1
      else
        If they are not equal then max of dp[i][j] = max(dp[i-1][j], dp[i][j-1])
        dp[i-1][j] --> exclude i character from string s
        dp[i][j-1] --> exclude j character from string t
```

### _Longest Path_

Problem :

There is a directed graph G with N vertices and M edges and is acyclic. Find the length of the longest directed path in G. Here, the length of a directed path is the number of edges in it.

```
1. How many states will be there in my dp ?
** There will be 1 state

2. What does each state in my dp represent ?
** dp[i] represents the longest length up until that node.

3. How do we transition to new state, i.e how do we compute dp[i] using previous values ?
** The transition rules are as follows

    for ( neighbour in current_vertex.getNeighbours() ) {
        // dp transition
        dist[neighbour] = max(dist[neighbour], dist[current_vertex] + 1)
        indegree[neighbour]--;
       
        if (indegree[neighbour] == 0 ) {
            dfs(indegree[neighbour])
        }
    }
```

Keeping track of indegree will help us avoid evaluating vertices that we already visited. Using this technique we will only move to a vertex if it is not visited or has indegree 0.

For example consider the following example to see the difference

%\!\(EXTRA markdown.ResourceType=, string=, string=\)

**Grid Problem**

problem:

[https://atcoder.jp/contests/dp/tasks/dp_h](https://atcoder.jp/contests/dp/tasks/dp_h)

```
* What are the states of dp ?
We keep track of number of ways to reach i row and j column, so we 2 states

* What does each state in dp represent ?
dp[i][j] represents number of ways to reach i row and j column.

* How to transition to new state, i.e how do we compute dp[i] using
previous values ?
dp[i+1][j]  = dp[i+1][j] + dp[i][j]
dp[i][j+1] = dp[i][j+1] + dp[i][j]
```

**Coins Problem**

problem:

[https://atcoder.jp/contests/dp/tasks/dp_i](https://atcoder.jp/contests/dp/tasks/dp_i)

```
* How many states will be there in my dp ?
There will be 2 states

* What does each state represent ?
dp[i][j] represents the probability to get i heads for j tails

* How to transition to new state, i.e how do we compute dp[i] using
previous values ?

if (j==0) {
  dp[i][j] = dp[i-1][j] * (1.0-p_heads[i-1]);
} else {
  dp[i][j] = dp[i-1][j] * (1.0-p_heads[i-1]) +  dp[i-1][j-1] * (p_heads[i-1]);
}
```

**Odd Subarrays**

problem:

[https://codeforces.com/problemset/problem/1686/B](https://codeforces.com/problemset/problem/1686/B)

```
* How many states will be there in my dp ?

We are only concerned about present element and weather it is smaller than the previous element

* What does each state represent ?

dp[i] represents the maximum number of odd subarrays that can be formed by considering arr[1:p] elements

* How to transitionto new state, i.e how do you compute dp[i] using previous values ?

Every odd subarray of length >=3 can be split into several small odd subarrays of length 2.

dp[i] = max( maximum odd subarray upto i-1, maximum subarray upto i-2 + (a[i-1] > a[i]))
```

## **K\- stones**

```
https://atcoder.jp/contests/dp/tasks/dp_k

1. What matters so far ?
-> We care about 2 things at any given moment. Who is playing and how many stones are left.

2. How many states does my dp have ?
-> We will have one state dp[i], where dp[i] represents if the current player win or not when there are i stones.

3. How do we transition to new state

-> for x in arr:
	 if (!dp[i-x]) // if current player is have i, and chooses x and if dp[i-x] is false then player wins at dp[i]
	 	dp[i] = true;
```

### **Knapsack DP**

```
Knapsack dp

https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/

what is important so far ?
-> the profit till now and weight left in the knapsack

What are the states of my dp ?
-> dp[i][c] represents the maximum value that be obtained for first i items for capacity c

How to transition to new state ?

for (int item_range=0;item_range<arr;item_range++)  { // Items to include from 0...items
	for(int cap=0;cap<=C;cap++) {	// Capacity, ensure c < C

		if (cap-weight[i] >= 0 ) {
			dp[item][cap] = max(dp[i-1][cap], profits[i] + dp[i][cap - weight[i]]);
		}
	}
}
```

**Given an array of numbers, find if a sum s can be obtained by add any of these numbers.**

1. Sort the array in ascending order
2. Compute prefix sum of the array
3. Binary search over the prefix array to find the sum

```
int left_index=-1, right_index=-1;

for(int l=0;l<n;l++) {
      int low = l;
      int high = n-1;
      int pos = -1;     

      while(low <= high) {
        int mid = low + (high - low)/2;

        int psum = prefix_sum[mid] - (l ? prefix_sum[l-1] :0);

        if (psum > k) {         
          high = mid-1;
        } else if (psum < k) {         
          low = mid+1;
        } else if (psum == k) {
          left_index = low;
          right_index = mid;
          break;
        }
      }                                   
}
cout<<left_index<<" "<<right_index<<endl;
```

## **C. An impassioned circulation of affection**

[https://codeforces.com/problemset/problem/814/C](https://codeforces.com/problemset/problem/814/C)

```
dp[i][j] represents the max length of subsequence for i'th letter with m replacable count.
```

DP problem with prefix max method

**Find possible sums when given an array of numbers**

```
    int n;

    cin >> n;

    vector<int> nums(n);
    ll sum = 0;

    for (int i = 0; i < n; i++)
    {
        cin >> nums[i];
        sum += nums[i];
    }

    vector<int> dp(sum + 1);
    dp[0] = 1;
    for (int i = 0; i < n; i++)
    {
        for (int j = sum; j >= nums[i]; j--)
        {
            dp[j] += dp[j - nums[i]];
        }
    }

    for (int i = 1; i <= sum; i++)
    {
        cout << i << " " << dp[i] << endl;
    }
```
