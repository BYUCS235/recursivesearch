# recursivesearch
In this learning activity, we will gain experience with searching for values recursively. To start with, lets create a vector of random integers that we can search through for particular values.
```c++
#include <iostream>
#include <vector>
#include <stdlib.h>
using namespace std;

int main()
{
  vector <int> myvec;
  
  int vecsize;
  cin >> vecsize;
  // Initialize the vector with random values
  for(int i = 0; i < vecsize; i++) {
    int nextval = rand() % vecsize;
    myvec.push_back(nextval);
  }
  // Print out the vector values
  for(auto val : myvec) {
    cout << val<< " ";
  }
  cout << endl;
}
```
Notice that we are using a different form of the for loop to print out the values.  This will work with most of the containers in C++.
Lets write a recursive function that will search through the vector for a value.  Remember that we need a base case and a recursive step that will reduce the size of the problem.  Since the problem is reduced in size by one each recursion, this is an O(n) algorithm.
```c++
int search(int sval, vector <int> &svec, int spos) {
  // Base Cases
  if(svec[spos] == sval)
    return spos;
  if(spos >= svec.size())
    return -1;
  // Recursive call with a smaller problem size
  return search(sval,svec,spos+1);
}
```
But what if we have a sorted list, can we do something better?  We ought to be able to break the vector in half every time and only look in the half where the value might be.  In this case we reduce the complexity to O(logn).
```c++
template<typename Item_Type>
int binary_search(const std::vector<Item_Type>& items, 
    int first, int last, const Item_Type& target) {
  if (first > last)
    return -1;     // Base case for unsuccessful search.
  else {
    int middle = (first + last) / 2;  // Next probe index.
    if (target == items[middle])
      return middle;   // Base case for successful search.
    else if (target < items[middle])
      return binary_search(items, first, middle - 1, target);
    else
      return binary_search(items, middle + 1, last, target);
  }
}
```
Notice that we are creating a template function that will work on any type that implements the "==" operator.  Templates can apply to functions, not just classes.
