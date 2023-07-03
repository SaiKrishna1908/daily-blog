---
title: Tree's Data Structure
date: '2020-09-03'
tags: ['trees', 'competative programming', 'C++']
draft: false
summary:
images: []
layout: PostLayout
canonicalUrl:
---

# Tree's

## Segment Tree

Segment tree stores information about an array in a tree which enables us to answer range

queries in logarithmic time.

a = \[1, 3, \-2, 8, \-7\]
%\!\(EXTRA markdown.ResourceType=, string=, string=\)

```
  struct segtree {

  int n;

  vector<int> t;

  segtree(int N) {

      n = N+1;
      t.assign(4*n+1,0);

  }

    void build(int a[],int v,int l, int r) {

      if(l == r) {
        a[v] = a[l];
      }

      else {
        int mid = (l+r) /2;
        build(a,v*2, l, mid);
        build(a,v*2+1, mid+1,r);

        a[v] = a[v*2] + a[v*2+1];
      }

  }

  int sum(int v, int l, int r, int tl, int tr) {

      if (l > r) {
        return 0;
      }

      if (l==tr && r==tr) {
        return t[v];
      }

      int tm = (tl + tr) /2;

      return sum(v,l,min(r,tm),tl, tm) + sum(v,max(l,tm+1),r,tm+1,tr);

  }

  void update(int v, int tl,int tr, int pos, int new_val) {

      if(tl == tr) {
        t[v] = new_val;
      }

      else {

        int tm = (tl + tr) /2;

        if(pos <= tm) {
      update(v*2, tl, tm,pos,new_val);
        }
        else {
      update(v*2+1, tm+1, tr,pos,new_val);
        }

        t[v] = t[v*2] + t[v*2+1];
      }

  }

  };
```

## Binary Index Tree \(or\) Fenwick Tree

- BIT can be used to perform a group function over a range of elements i.e f\(A1, A2, A3 ..., Ar\) in O\(logn\) time.
- Updates to array, and propogation of changes take place also in O\(logN\) time.

Example: BIT can be used to calculate perfix sum array in O\(logN\) time. If we use naive     array approach it takes O\(N\) to update the array.

[https://www.youtube.com/watch?v=9uaXG62Y8Uw](https://www.youtube.com/watch?v=9uaXG62Y8Uw)

```
struct BIT {

  int n;
  vector<int> bit;

  BIT(int N) {

      n = N;
      bit.assign(N+1,0);

  }

  void update(int i, int v) {
  while( i<=n ) {

        bit[i] = (bit[i] + v)%mod;

        i += i & (-i);
      }

  }

  int query(int i) {

    int res = 0;

    while (i>0) {

      res = (res+bit[i])%mod;
   
      i-=i & (-i);
    }
   
        return res;
    }
  };
```

## Post Order Traversal Iterative Approach

```
Tree *tree

stack<*Node> st;
stack<int> outstack;

st.push_back(tree->root);

while(!st.empty()) {
    Node* top = st.top();

   
    for(child : top) {
        st.push(child);
    }

    outstack.push(top);

    st.pop();
}
```

## DP with Tree's

1. [https://cses.fi/problemset/task/1131](https://cses.fi/problemset/task/1131)

The above problem can be solved using DP.

1. How many states will be there in my dp ?
2. What does each state in my dp represent ?
3. How do we transition to new state, i.e how do we compute dp\[i\]  using previous values ?

4. We will have 2 dp states dp\[i\]\[j\]
5. dp\[i\]\[j\] where i takes all the possible node values and j can be 0 or 1.

```

         1
        / \
       3   2
      / \
     4   5

What is dp[i][0] ?

The maximum diameter in the subtree starting at node i, where i is involved and also i is the endpoint of the path

dp[3][0] = 4->3

What is dp[i][1] ?

The maximum diameter in the subtree starting at node i, where i is involed but not necessarly the endpoint of the path.

dp[3][1] = 4->3->5
```

1. Transition is as follows

```
dp[i][0] = max(1+dp[v][0]) // where v is a child of node i.

dp[i][1] = max(1+dp[v1][0] + 1 + dp[v2][0]) // where v1 and v2 are the children of node i with max diameter
```

1. [https://codeforces.com/problemset/problem/1083/A](https://codeforces.com/problemset/problem/1083/A)

A good problem for DP with Tree.
