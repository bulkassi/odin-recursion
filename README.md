# odin-recursion

This repository presents an answer to the [Project: Recursion](https://www.theodinproject.com/lessons/javascript-recursion) tasks. 

## Fibonacci

The iterative approach to tackling a Fibonacci sequence:
```js
function fibs(n) {
  if (n === 0) {
    return 0;
  }
  if (n === 1) {
    return 1;
  }
  
  let first = 0;
  let second = 1;
  let next = 1;
  for (let i = 1; i < n; i++) {
    next = first + second;
    first = second;
    second = next;
  } 
  
  return next;
}
```
Both worst-case and average-case running times of iterative approach to calculating the n-th number of Fibonacci sequence is $O(n)$, since the size of the loop is linear in terms of $n$, and all other operations take constant time $O(1)$.

The recursive approach:
```js
function fibsRec(n) {
  if (n <= 1) {
    return n
  }
  
  return fibsRec(n - 1) + fibsRec(n - 2)
}
```
Both worst-case and average-case running times of recursive approach to calculating the n-th number of Fibonacci sequence is $O(2^n)$ - the size of the binary recursion tree grows exponentially with $n$.

## Merge sort

The merge sort algorithm using JS (sorting is done in non-decreasing order):
```js
function merge(arr, q) {
  let L = arr.slice(0, q);
  let R = arr.slice(q);
  L.push(Number.POSITIVE_INFINITY);
  R.push(Number.POSITIVE_INFINITY);
  
  let i = 0;
  let j = 0;

  for (let k = 0; k < arr.length; k++) {
    if (L[i] <= R[j]) {
      arr[k] = L[i];
      i += 1;
    }
    else {
      arr[k] = R[j];
      j += 1;
    }
  }
  
  return arr;
}

function mergeSort(arr, p, r) {
  if (p < r) {
    q = Math.floor((p + r) / 2);
    mergeSort(arr, p, q);
    mergeSort(arr, q + 1, r);
    merge(arr, q);
  }
}
```
The `merge` function sorts the entire array given that its subarrays `arr[0, q - 1]` and `arr[q, arr.length]` are already sorted. The `mergeSort` then incorporates it to recursively divide the initial array and then subarrays into smaller ones and merging them. The divisions stop at arrays of length 1, which are trivially sorted. Both worst-case and average-case running times of the `mergeSort` are $O(n \ln{n})$
