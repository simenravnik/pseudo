
# ALGORITMI IN PODATKOVNE STRUKTURE 2

```
Ta datoteka vsebuje pseudokode algoritmov, ki smo jih
spoznali na vajah.

Avtor: Simen Ravnik
Datum: June, 2019

Nosilec predmeta: prof. dr. Borut Robic

Note: Pseudokode niso moje avtorsko delo, bile so
      poiskane na internetu in zdruzene v ta file.
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

```
for i from 1 to N
    select some vertex v with indegree(v) equal to 0
    add v to our topological sort
    remove v and all edges leading from it
```

### BELLMAN - FORD
***`O(n^3)`***

```
BEGIN
	FOR ALL V=!S,D[V]=~;
	   D[S]=0;
	     FOR ALL V,  X[V]=NIL;
	     FOR STEP =1 TO N;
	      FOR(U,V) BELONGS TO E;
	        IF (D[W]+W[U,V]< D[V])
	            D[V] =D[W]+W[U,V]<D[V]);
	            X[V]=U;
END;
```

### FLOYD - WARSHALL
***`O(n^3)`***

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