# C++ Basics & Helper Snippets

## Convert char to int

```
'0' -> 0

char a = '4';
int ia = a - '0';

Ascii value of a
char a = 'a';
int ia = (int)a;
```

## Find Max of more than 2 elements

```
int res = max({1,2,3,4,5});
```

## Get middle element when two elements are int

```
int mid = low + (high - low) /2;
```

## Create a Comparator and use it with a set

```
auto cmp = [] (pair<int,int> const &x, pair<int,int> const &y) {
if (x.second != y.second)
return x.second > y.second;

    return x.first > y.first;

};
set<pii, decltype(cmp)> a(cmp);
```

## Sorting Vector using Lamba

```
vints[i].sort([&words](int i, int j) { return words[i] < words[j]; });

(or)

vector<pair<char,int>> mapl(n);
sort(mapl.begin(),mapl.end(),[](auto i,auto j) { return i.first < j.first;});
```

Fill an array with a number

```
int dp[n+1];

fill(dp, dp+n+1, -1e8);
```

## Fill 2D arrays with \-1

```
int dp[n][m];

fill(&dp[0][0], &dp[0][0]+sizeof(dp), -1);
```

## Find minimum element in vector

```
int min = *min_element(a.begin(), a.end())
```

## Vector Basics

Defining a vector:

```
vector<int> v;
```

Vector methods:

1. **vector.size\(\)** Returns the number of elements in vector.
2. **vector.begin\(\)** Returns an iterator pointing to the first element in vector.
3. **vector.end\(\)** Returns an iterator pointing to the theoretical element that follows the last element in the vector.
4. **vector.push_back\(val**\) Push element \(val\) into the vector from back.
5. **vector.empty\(\)** Returns whether vector is empty.

### remove :

```
#include<bits/stdc++.h>
using namespace std;
int main(){
    vector<int> v;
    //Insert values 1 to 10
    v.push_back(20);
    v.push_back(10);
    v.push_back(30);
    v.push_back(20);
    v.push_back(40);
    v.push_back(20);
    v.push_back(10);

    vector<int>::iterator new_end;
    new_end = remove(v.begin(), v.end(), 20);

    for(int i=0;i<v.size(); i++){
        cout << v[i] << " ";
    }
    //Prints [10 30 40 10]
    return 0;
}
```

### remove_copy :

```
#include <bits/stdc++.h>

using namespace std;

int main()
{
    vector<int> v1 {10,20,10,30,20,20,30,10};
    vector<int> v2(8);
    remove_copy(v1.begin(), v1.end(), v2.begin(), 20);

    for(int i=0;i<v2.size();i++){
        cout << v2[i] << " ";
    }
    //Prints[10,10,30,30,10,0,0,0]
    return 0;
}
```

### remove_if :

```
#include<bits/stdc++.h>
using namespace std;

bool isEven(int k){
    return ((k%2) == 0);
}

int main(){

    vector<int> v {1,2,3,4,5,6,7,8,9,10};
    //Initially the vector contains elements from 1 to 10.
    vector<int>::iterator it;
    it = remove_if(v.begin(), v.end(), isEven);
    //isEven() method checks each element whether it is even or not.

    for(int i=0;i<v.size(); i++){
        cout << v[i] << " ";
    }
    //Print the elements in vector
    //[1,3,5,7,9]

    return 0;
}
```

### erase :

```
vector.erase(position)
// or
vector.erase(left,right) // *([left,right))*
```

### initialize 2d vector

```
 vector<vector<int>> dp(n, vector<int>(k,0));
```

##

## Map in C\+\+

```
map<long, long> am;

    for (int i = 0; i < n; i++)
    {
      int in;
      cin >> in;
      if (am.find(in) != am.end())
      {
        am[in] += 1;
      }
      else
      {
        am[in] = 1;
      }
    }
```

## Remove an element from a vector and preserving the original vector :

```
vector<int> v1(n);
vector<int> v2(n);

remove_copy(v1.begin(), v1.end(), v2.begin(), val);
auto itr = remove(v2.begin(), v2.end(), 0);
v2.erase(itr, v2.end());

// Now v2 has elements removed val from v1
```

**Compute Ceil of division without using function** :

```
int ceil = (x/y) + ((x%y) != 0);
```

##

## **Compute Ceil to Floor**

```
⌈a / b⌉ = ⌊(a + b−1) / b⌋
```

##

Proof: https://math.stackexchange.com/questions/448300/convert\-ceil\-to\-floor

##

## **Lower bound and Upper bound in C\+\+**

```
// For lower_bound if we pass a value the returned elements will not be less than val
// ie element[i] >= val

// For upper_bound unlike lowerbound only elements strightly greater than val are returned
// ie element[i] > val
```

```
int myints[] = {10,20,30,30,20,10,10,20};
  std::vector<int> v(myints,myints+8);           // 10 20 30 30 20 10 10 20

  std::sort (v.begin(), v.end());                // 10 10 10 20 20 20 30 30

  std::vector<int>::iterator low,up;
  low=std::lower_bound (v.begin(), v.end(), 20); //          index 3
  up= std::upper_bound (v.begin(), v.end(), 20); //          index 6   
```

#

**Note:** To print lower bound use lower_bound\(v.begin\(\), v.end\(\), a\[i\]\) \- v.begin\(\)

**Initializing 2D array to a constant**

```
int a[10][10] = {{0}}

bool b[200][200] = {{ false }}
```

**Multiset in C\+\+**

```
A Multiset is a data structure which stores elements in sorted order similar to a Set. In contrast to Set, a multiset can contain duplicate values

declaration:

multiset<int> a;

insert:

a.insert(1);
a.insert(2);
a.insert(1);
```
