---
title: "Algoritmi"
author: Simen Ravnik
date: June 4, 2019
---


# ALGORITMI IN PODATKOVNE STRUKTURE 2

```
Ta datoteka vsebuje pseudokode algoritmov, ki smo jih
spoznali na vajah.

Avtor: Simen Ravnik
Datum: June, 2019

Nosilec predmeta: prof. dr. Borut Robic
```

> *Note: Pseudokode niso moje avtorsko delo.*

---
## Big O Notation

$$ O(g(n))={f(n) ∣ ∃c, n_0 >0∀ n≥n_0 :0 ≤ f (n) ≤ cg(n)} $$

$$ Ω(g(n))={f (n) ∣ ∃c ,n_0 >0∀n≥n_0 :0≤cg(n)≤f (n)} $$

$$ Θ(g(n))={f(n) ∣∃c_1 ,c_2,n_0>0∀n≥n_0:0≤c_1 g(n)≤f(n)≤c_2g(n)} $$

***Z limitami:***

```math
f(n)=O(g(n)):
\quad
{\displaystyle \limsup _{n\to \infty }{\frac {\left|f(n)\right|}{g(n)}}<\infty }
```

```math
f(n)=\Omega (g(n)):
\quad
{\displaystyle \liminf _{n\to \infty }{\frac {f(n)}{g(n)}}>0}
```

```math
f(n)=\Theta (g(n)):
\space
f(n)=O(g(n)) \space and \space
f(n)=Ω(g(n))
```

---

## Sorting algoritmi

### BUBBLE SORT
***`O(n^2)`***
```
swapped = true
   while swapped
      swapped = false
         for j from 0 to N - 1
            if a[j] > a[j + 1]
               swap( a[j], a[j + 1] )
               swapped = true
```

### SELECTION SORT
***`O(n^2)`***

```
func selectionSort(list)
   max = length(list) - 1

   for i from 0 to max
      key = list[i]
         keyj = i

         for j from i+1 to max
            if list[j] < key
               key = list[j]
               keyj = j

         list[keyj] = list[i]
         list[i] = key
    return list
end func
```
### INSERTION SORT
***`O(n^2)`***

```
for i from 1 to N
   key = a[i]
   j = i - 1
   while j >= 0 and a[j] > key
      a[j+1] = a[j]
      j = j - 1
   a[j+1] = key
```

### HEAP SORT
***`O(nlogn)`***

```
Heapsort(A as array)
    BuildHeap(A)
    for i = n to 1
        swap(A[1], A[i])
        n = n - 1
        Heapify(A, 1)

BuildHeap(A as array)
    n = elements_in(A)
    for i = floor(n/2) to 1
        Heapify(A,i,n)

Heapify(A as array, i as int, n as int)
    left = 2i
    right = 2i+1

    if (left <= n) and (A[left] > A[i])
        max = left
    else
        max = i

    if (right<=n) and (A[right] > A[max])
        max = right

    if (max != i)
        swap(A[i], A[max])
        Heapify(A, max)
```

### MERGE SORT
***`O(nlogn)`***

```
func mergesort( var a as array )
     if ( n == 1 ) return a

     var l1 as array = a[0] ... a[n/2]
     var l2 as array = a[n/2+1] ... a[n]

     l1 = mergesort( l1 )
     l2 = mergesort( l2 )

     return merge( l1, l2 )
end func

func merge( var a as array, var b as array )
     var c as array

     while ( a and b have elements )
          if ( a[0] > b[0] )
               add b[0] to the end of c
               remove b[0] from b
          else
               add a[0] to the end of c
               remove a[0] from a
     while ( a has elements )
          add a[0] to the end of c
          remove a[0] from a
     while ( b has elements )
          add b[0] to the end of c
          remove b[0] from b
     return c
end func
```

### QUICK SORT
***`O(nlogn)`***

```
Quicksort(A as array, low as int, high as int){
    if (low < high){
        pivot_location = Partition(A,low,high)
        Quicksort(A,low, pivot_location)
        Quicksort(A, pivot_location + 1, high)
    }
}
Partition(A as array, low as int, high as int){
     pivot = A[low]
     leftwall = low

     for i = low + 1 to high{
         if (A[i] < pivot) then{
             swap(A[i], A[leftwall + 1])
             leftwall = leftwall + 1
         }
     }
     swap(pivot,A[leftwall])

    return (leftwall)
}
```
### COUNTING SORT
```
TO DO...
```

### RADIX SORT
```
TO DO...
```

---
## Mnozenje stevil

### MNOZENJE DELI IN VLADAJ
```
Algorithm Divide-Mult(a,b):
if a or b has one digit, then:
    return a * b.
else:
    Let n be the number of digits in max{a, b}.

    Let aL and aR be left and right halves of a.
    Let bL and bR be left and right halves of b.

    Let x1 hold Divide-Mult(aL, bL).
    Let x2 hold Divide-Mult(aL, bR).
    Let x3 hold Divide-Mult(aR, bL).
    Let x4 hold Divide-Mult(aR, bR).

    return x1*10n + (x2 + x3)*10n/2 + x4.
end of if
```

### KARATSUBA
```
procedure karatsuba(num1, num2)
  if (num1 < 10) or (num2 < 10)
    return num1*num2

  /* calculates the size of the numbers */
  m = min(size_base10(num1), size_base10(num2))
  m2 = floor(m/2)
  /*m2 = ceil(m/2) will also work */

  /* split the digit sequences in the middle */
  high1, low1 = split_at(num1, m2)
  high2, low2 = split_at(num2, m2)

  /* 3 calls made to numbers approximately half the size */
  z0 = karatsuba(low1, low2)
  z1 = karatsuba((low1 + high1), (low2 + high2))
  z2 = karatsuba(high1, high2)

  return (z2 * 10 ^ (m2 * 2)) + ((z1 - z2 - z0) * 10 ^ m2) + z0
```

---
## Mnozenje matrik

```
# iterate through rows of X
for i in range(len(X)):
   # iterate through columns of Y
   for j in range(len(Y[0])):
       # iterate through rows of Y
       for k in range(len(Y)):
           result[i][j] += X[i][k] * Y[k][j]
```

### DELI IN VLADAJ
`TO DO...`

### STRASSEN
`TO DO...`

---
## Ostali

### BINARY SEARCH
***`O(logn)`***

```
search(a, left, right, x)
    if left > right then
        return -1
    mid := left+floor((right-left) / 2)
    if a[mid] = x then
        return mid
    else if a[mid] > x then
        return search(a, left, mid-1, x)
    else
        return search(a, mid+1, right, x)
```

### TOPOLOSKO UREJANJE
***`O(|v|^2)`***

> Uredimo lahko samo aciklicne grafe.
> "Po povezavah narascajo tudi oznake vozlisc."

```
for i from 1 to N
    select some vertex v with indegree(v) equal to 0
    add v to our topological sort
    remove v and all edges leading from it
```

### BELLMAN - FORD
***`O(n^3)`***

> Shortest path

```
for v in V:
    v.distance = infinity
    v.p = None
source.distance = 0
for i from 1 to |V| - 1:
    for (u, v) in E:
        if v.distance > u.distance + weight(u, v):
            v.distance = u.distance + weight(u, v)
            v.p = u
for (u, v) in E:
    if v.distance > u.distance + weight(u, v):
        print "A negative weight cycle exists"
```

### FLOYD - WARSHALL
***`O(n^3)`***

> Shortest path

```
for i = 1 to N
 for j = 1 to N
    if there is an edge from i to j
       dist[0][i][j] = the length of the edge from i to j
    else
       dist[0][i][j] = INFINITY

for k = 1 to N
   for i = 1 to N
      for j = 1 to N
         dist[k][i][j] = min(dist[k-1][i][j], dist[k-1][i][k] + dist[k-1][k][j])
```

### FFT
***`O(nlogn)`***

```
fun recursiveFFT(a) is
	n = a.length
	if n == 1 then return a
	ys = recursiveFFT([a , a , ..., a ])
	yl = recursiveFFT([a , a , ..., a ])

	w = e^(2 PI i / n)
	wk = 1
	y = [0, 0, ..., 0]
	for k = 0 to n/2­1 do
		y[k] = ys[k] + wk * yl[k]
		y[k+n/2] = ys[k] – wk * yl[k]
		wk = wk * w
	end
	return y
end
```

### 01 nahrbtnik
```
for j from 0 to W do:
      m[0, j] := 0

for i from 1 to n do:
  for j from 0 to W do:
      if w[i] > j then:
          m[i, j] := m[i-1, j]
      else:
          m[i, j] := max(m[i-1, j], m[i-1, j-w[i]] + v[i])
```

### k'th smallest element
```
def kthSmallest(arr, l, r, k):

    # If k is smaller than number of  
    # elements in array
    if (k > 0 and k <= r - l + 1):

        # Partition the array around last  
        # element and get position of pivot
        # element in sorted array
        pos = partition(arr, l, r)

        # If position is same as k
        if (pos - l == k - 1):
            return arr[pos]
        if (pos - l > k - 1): # If position is more,  
                              # recur for left subarray
            return kthSmallest(arr, l, pos - 1, k)

        # Else recur for right subarray
        return kthSmallest(arr, pos + 1, r,
                            k - pos + l - 1)

    # If k is more than number of
    # elements in array
    return sys.maxsize
```
```
# Standard partition process of QuickSort().  
# It considers the last element as pivot and
# moves all smaller element to left of it
# and greater elements to right
def partition(arr, l, r):

    x = arr[r]
    i = l
    for j in range(l, r):
        if (arr[j] <= x):
            arr[i], arr[j] = arr[j], arr[i]
            i += 1
    arr[i], arr[r] = arr[r], arr[i]
    return i
```
