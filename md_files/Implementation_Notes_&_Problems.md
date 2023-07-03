# Implementation Notes & Problems

## **Prefix Sum**

Prefix sum can be used to calculate sum of a interval in an array in O\(1\) time.

```
* Indexing is from 0

Consider the array = [3,1,5,2,7]

* Prefix sum size is n+1

prefix_sum = [0,3,4,9,11,18]

To get prefix_sum from interval [2,4]

ans = prefix_sum[4+1] - prefix_sum[2] ; ie 18 - 4 = 14
```

#

```
Prefix sum with size n

consider array = [3,1,5,2,7]
prefix_sum = [3,4,9,11,18]

To get prefix_sum from interval [2,4]

int psum = prefix_sum[4] - (2 ? prefix_sum[2-1] :0);  ie 18 - 4 = 14
```

#

## **Cyclic Rotation**

```
Cyclic rotation - two pointer method

-> let i = 0, j = a.length - 1
-> iterate from i = 0 to i<j and swap a[i] with a[j]

    1 2 3 4 5
->  5 2 3 4 1
->  5 1 3 4 2
->  5 1 2 4 3
->  5 1 2 3 4  // Rotation complete, took one step left

C++ rotate method

rotate(<beginning_of_array>, <element_that_should_appear_first>, <end_of_array>)

rotate(a.begin(), a.begin()+1,a.end())  // 1 2 3 4 -> 2 3 4 1
```

## **How to check interval intersection between co\-ordinates/points**

```
This problem is based on finding intersection of interval's   

intersection between (ai, bi) (aj, bj) (ak, bk) can be found by following technique

left_intersection = max(ai, aj)
right_intersection = min(bi, bj)

(left_intersection, right_intersection) -> new interval which

left_intersection = max(ak, left_intersection)
right_intersection = min(bk, right_intersection)

How do we know if there is no intersection ?

-> At any point if left_intersection > right_intersection, there is not intersection
```

## **Notes on GCD & LCM**

LCM \(a, b\) =  \(a \* b\) / GCD\(a,b\)

## **Fighting Tournament**

\( [https://codeforces.com/problemset/problem/1719/C](https://codeforces.com/problemset/problem/1719/C) \)

A good implementation problem.

```
https://codeforces.com/contest/1719/submission/170859071
```

### **Mark and His Unfinished Essay**

**\([https://codeforces.com/problemset/problem/1705/C](https://codeforces.com/problemset/problem/1705/C)\)**

A good implementation problem

## **Sieve of Eratosthenes**

Sieve of Eratosthenes if one of the efficient ways to find all primes smaller than n when n is smaller than 10 million.

```
// true if i is prime
// false if i is composite
bool primes[n+1]

memset(primes, true, sizeof(prime));

for(int p=2;p * p <= n; p++) {
    if (primes[p] == true) {
        for(int i=p*p;i<=n;i+=p) {
            prime[i] = false;
        }
    }
}
```

## **Linear Sieve**

Linear Sieve has a side effect where it calculates the minimum prime factor for every number i in the segment \[2,n\].

The final array looks like this.

\[1, 2, 3, 2, 5, 2, 7, 2, 3....\]

from above array if a\[i\] == i \(or\) a\[i\] = \-1 then it is a prime number. If not, then that number is the least prime which divides that number

```
const int N = 10000000;

vector<int> lp(N)

fill(lp, lp+N, -1);

lp[1] = 1;

for(int i=2;i*i< N;i++) {
   // is prime if lp[i] = -1
   if (lp[i] == -1) {
        lp[i] = i;
       
        for(int j= i * i;j < N;j += i) {
            if (lp[j] == -1) {
                lp[j] = i;
            }
        }
    }
}
```

##

## **Interval Scheduling Problem**

You have n tasks to complete and each task has a start time and end time to complete. What is the maximum number of tasks

which can be completed ?

```
https://cses.fi/problemset/task/1629
```

Algorithm:

1. Sort the tasks by end in ascending order
2. For each task if previous end_time is greater than start_time of current task, we cannot do the current task

```
sort(events.begin(), events.end(), [](pair<int,int> i, pair<int,int> j) {
     return i.second < j.second;
});

int prev_et = -1;
int count = 0;

for(int i=0;i<n;i++) {
  if (events[i].first >= prev_et) {
    count++;
    prev_et = events[i].second;
  }
}

cout<<count<<endl;
```

## **How to keep an array sorted ?**

Use a Priority Queue, a priority queue will keep all the elements sorted while insertion.

```
// C++ program to demonstrate the use of priority_queue
#include <iostream>
#include <queue>
using namespace std;

// driver code
int main()
{
	int arr[6] = { 10, 2, 4, 8, 6, 9 };

	// defining priority queue
	priority_queue<int> pq;

	for (int i = 0; i < 6; i++) {
		pq.push(arr[i]);
	}

	// printing priority queue
	cout << "Priority Queue: ";
	while (!pq.empty()) {
		cout << pq.top() << ' ';
		pq.pop();
	}

	return 0;
}

Output

Priority Queue: 10 9 8 6 4 2
```

##

**Monotonic Stack**

A Monotonic Stack is a stack which stores elements in certain order. The order must be preserved while maintaining the stack

[https://itnext.io/monotonic\-stack\-identify\-pattern\-3da2d491a61e](https://itnext.io/monotonic-stack-identify-pattern-3da2d491a61e)

Problem:

[https://cses.fi/problemset/task/1645/](https://cses.fi/problemset/task/1645/)

**Modular Exponentiation**

```
This function calculates the modular inverse.
To calculate the following equation, call this function.
(a/b) % MOD
(a * modularBinaryExponentiation(b, MOD-2)) % MOD;

ll modularBinaryExponentiation(int base, int exponent) {
  if(exponent == 0)
    return 1;

  ll result = modularBinaryExponentiation(base, exponent/2);

  if (exponent%2 == 1)
    return (((result * result) % MOD) * base ) % MOD;
 
  else
    return (result  * result) % MOD;
}
```

## **Math Notes**

# **What is a Multiset ?**

```
A multiset is a modification of the concept of a set that, unlike a set, allows for multiple instances for each of its elements.
 The number of instances given for each element is called the multiplicity of that element in the multiset.

example: a = {1, 2, 2, 3, 3, 4}
```

# P, NP, NP\-Complete, NP\-Hard

- P is a set of problems which can be solved in Polynomial\-Time
- NP is a set decision problems that can be solved by Non\-Deterministic Turing Machine in Polynomial Time
