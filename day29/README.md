![cover](./cover.png)

# Day 29 - Search and Sort Algorithms Part B: The Binary Search

Binary Search is searching technique which works on Divide and Conquer approach. Indeed an efficient searching algorithm with a runtime of `O(log(n))`, but it works only on sorted arrays.

## Question

Given a sorted array, and a number n, write a program to implement binary search and finid the index of the given number.

Try to do it using recursion as well as iteration.

**Example**

```
input: arr = [1, 2, 3, 4, 5, 8, 9], num = 8
output: 5 (index of found element)

input: arr = [1, 2, 3, 4, 5, 8, 9], num = 7
output: undefined
```

![ques](./ques.png)

## Solution

### [JavaScript Implementation](./JavaScript/binary.js)

```js
function binary (arr, n) {
    let left = 0,
        right = arr.length - 1, mid;

    while (left <= right) {
        mid = Math.floor((left + right)/2);
        if (arr[mid] === n)  return mid;
        else if (arr[mid] < n)  left = mid+1;
        else right = mid-1;
    }

    return -1;
}

console.log (binarySearch ([1, 2, 3, 4, 5, 8, 9], 8));
console.log (binarySearch ([1, 2, 3, 4, 5, 8, 9], 7));
```

## C++ Implementation

### [Solution by @imkaka](./C++/binary_search.cpp)

```cpp

/*
* @author : imkaka
* @date   : 31/1/2019
*/

#include<iostream>
#include<cstdio>

using namespace std;

int binary_search_itr(int arr[], int size, int val){
    int l = 0, r = size-1;
    int mid = (l + r) / 2;

    while(arr[mid] != val && l <= r){
        if(val < arr[mid]){
            r = mid - 1;
        }
        else{
            l = mid +1;
        }

        mid = (l + r) / 2;
    }

    if(arr[mid] == val)
        return mid;

    return -1;
}

int binary_search_rec(int arr[], int left, int right, int val){
    if(right >= left){

        int mid = left + (right - left) / 2;

        if(arr[mid] == val) return mid;

        if(arr[mid] > val)
            return binary_search_rec(arr, left, mid-1, val);
        return binary_search_rec(arr, mid+1, right, val);
    }

    return -1;
}

int main(){

    int arr[] = {1, 2, 3, 6, 9, 15, 16, 14};
    int val = 9;
    int size = sizeof(arr)/sizeof(arr[0]);
    cout << "Iterative: " << binary_search_itr(arr, size, val) << endl;
    cout << "Recursive: " << binary_search_rec(arr, 0, size-1, val) << endl;
    return 0;
}
```