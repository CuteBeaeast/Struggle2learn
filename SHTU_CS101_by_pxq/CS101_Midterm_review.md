# CS101_Midterm_review

by pxq

[TOC]

## 1.	Linked List

### 1)	implementation of Node and LinkedList class

* trivial

### 2)	operations and complexity

| operation     | complexity                   | notice                                                       |
| ------------- | ---------------------------- | ------------------------------------------------------------ |
| Find kth node | O(n)                         | theta(1) for 1st or nth node                                 |
| insert before | theta(1)                     | optimization required                                        |
| insert after  | theta(1)                     |                                                              |
| replace       | theta(1)                     |                                                              |
| erase         | theta(1),```O(n) for tail``` | optimization required                                        |
| next          | theta(1)                     |                                                              |
| previous      | O(n)                         | No trivial optimization, can be optimized using double linked list |

### 3)	optimizations of methods

#### a.	insert before

* insert after
* swap(& this->data, & this->next->data)

#### b.	erase

* swap(& this->data, & this->next->data)
* this->next = this->next->next
* remember to erase the original this->next

### 4)	comparison between linkedlist and array

* LinkedList: data with frequent modifications
* Array: fast accessing, stable data



## 2.	Stack and Queue

### 1)	operations

#### a.	Stack: LIFO

* push(at top)
* pop(from top)

#### b.	Queue: FIFO

* push(at back)
* pop(from top)

### 2)	implementation

#### a.	Stack

* singly linked list (front as top)

* one-ended array (back as top)
* optimal run time is theta(1) for any implementation

#### b.	Queue

* singly linked list(front as head and back as tail)


* two-ended array(circular)


### 3)	applications

#### a.	Stack

* Reverse-Polish Notation
* Function calls
* Parsing XHTML

#### b.	Queue

* nothing so far



## 3.	Algorithm Analysis

### 1)	Landau Symbols

#### a.	definitions

| Symbol                     | $$ \lim_{n\to\infin} \frac{f(n)}{g(n)} $$ | intuition (g is a balahbalah of f) |
| -------------------------- | ----------------------------------------- | ---------------------------------- |
| $$ f(n) = O(g(n)) $$       | $$ < \infin $$                            | asymptotic upper bound             |
| $$ f(n) = \Omega (g(n)) $$ | > 0                                       | asymptotic lower bound             |
| $$ f(n) = \Theta(g(n)) $$  | > 0 and $$ < \infin $$                    | asymptotic close bound             |
| $$ f(n) = o(g(n)) $$       | = 0                                       | more upper than $$ O $$            |
| $$ f(n) = \omega(g(n)) $$  | $$ = \infin $$                            | more lower than $$ \Omega $$       |

#### b.	some mathematical things

* nothing grows faster than exponential
* in ascending order: $$ const, log(n), n, n^2, 2^n $$
*  $$ 3^{2^n} = O(2^{3^n}) $$

### 2)	Solve for the time complexity of the recursive functions with substitution method

#### a.	procedures

* start with the lowest possible growth
* proof it is true
* if not true, start again with a faster growing function

####  b.	example

solve the time complexity for T(n) while:
$$
T(n) = T(\lfloor \frac{n}{2} \rfloor) + T(\lceil \frac{n}{2} \rceil) + 1
$$

* Guess: T(n) = O(1) and T(n) = O(log(n)), prove impossible.
* Guess: $$ T(n) = O(n) $$: $$ \exist c, d $$ such that $$ T(n) \leq cn - d $$
* Substitute: $$ T(n) \leq \lfloor \frac{n}{2} \rfloor - d + \lceil \frac{n}{2} \rceil - d + 1 = cn - d + (1 - d)$$
* True when $$ d \geq 1 $$
* So $$ T(n) = O(n) $$



## 4.	Bubble sort

### 1)	algorithm

* trivial

### 2)	optimizations

#### a.	flagged bubble sort

* a Boolean flag for "swap"
* if no swap happens, the sort is completed

#### b.	range-limiting bubble sort

* limit the range to where the last swap happened in the last loop

#### c.	alternating bubble sort

* alternatively bubble the biggest element up and smallest element down

### 3)	complexity

* cannot do any better than insertion sort



## 5.	Insertion sort

### 1)	concepts

#### a.	inversion

* a pair of entries which are reversed

### 2)	algorithm

```cpp
for(int k = 1; k < n; ++k)
{
    for (int j = k; j > 0; --j)
    {
        if(array[j - 1] > array[j])
            std::swap(array[j - 1]; array[j])
        else
            break;
    }
}
```

### 3)	complexity

* $$ O(n^2) $$
* n + d comparisons are performed, d being #inversions
* If #inversions = O(n), then time complexity will be O(n)
* In worst case, #inversions = $$ \frac{n(n-1)}{2} $$



## 6.	Tree

### 1)	Traverse

* order convention: from left to right

#### a.	BFS

* can be implemented using a Queue
* $$ \Theta(n) $$ time and o(n) memory

#### b.	DFS

* implemented using recursion or a Stack(inverse order push)
* $$ \Theta(n) $$ time and $$ \Theta(h) $$ memory 

#### c.	Pre/Post/In-ordering

* give traverse order given tree(trivial)

* rebuild tree given traverse order(trivial)



## 7.	Binary Tree

### 1)	definition and property

* binary tree: each node has at most 2 children
* full: nodes are leaves or full
* perfect: all leaf nodes have the same depth h and all other nodes are full
* complete: filled at each depth from left to right
* complete and full have nothing in relation

### 2)	heights

#### a.	in general

* worst case: $$ \Theta(n) $$
* best case: $$ \Theta(ln(n)) $$

#### b.	for perfect binary tree

* $$ n = 2^{h + 1} - 1 $$



## 8.	Binary Heap

### 1)	definitions and property

* binary heap: key in the root is smaller(bigger) than keys in the children, defined recursively for all child trees

### 2)	implementation

* better use complete binary tree
* put the root node in array[1]

### 3)	operations

#### a.	top

* trivial $$ \Theta(1) $$

#### b.	pop

* pop the root key
* move the last entry to the top
* maintain the property
* $$ O(ln(n)) $$

#### c.	push

* push at the back
* maintain property
* $$ O(ln(n)) $$ for worst case and O(1) for average

### 4)	Build Heap

#### a.	repeated performing push

* complexity: $$ O(n log(n)) $$ (n pushes, O(log(n)) for each)

#### b.	Floyd's Method

##### i.	procedures

* put the keys in a complete binary tree
* maintain the property(percolate down) for the first size/2 nodes

##### ii.	complexity

- $$ \Theta(n) $$
- Worst case: n/4 percolated down 1 level, n/8 percolated down 2 levels, ······

$$
T(n) = 1\frac{n}{4} + 2\frac{n}{8} + 3\frac{n}{16} + ··· = \sum_{i = 1}^{i = log(n)} i\frac{n}{2^{i + 1}} = \frac{n}{2} \sum_{i = 1}^{i = log(n)} \frac{i}{2^{i}} = n
$$

### 5)	Run time analysis for push

I personally thinks it is very counter-intuitive, so I put a separate title for it.

For the worst case, it takes O(log(n)) to perform push(trivial to prove).

However, in average case, it will be $$ \Theta(1) $$. The central idea is that the inserted node is equally possible to be at any node of the tree, and lower levels have more nodes. The proof is as follows.

* On average, with each percolation, an object will be moved past half or the entries in the tree.
* Therefore, for each push:

$$
T(n) = \frac{1}{n} \sum_{k = 0}^{h} (h - k) 2^k = \frac{2^{h + 1} - h - 2}{n} = \frac{n - h - 1}{n} = \Theta(1)
$$

### 6)	Heap sort

#### a.	procedures

* place all the object in to a heap(Floyd's method)
* repeatedly popping the top object until empty

#### b.	complexity

* build heap: $$ O(n) $$
* popping n objects: $$ O(n log(n)) $$
* total: $$ O(n log(n)) $$



## 9.	Binary Search Tree

### 1)	definition

* trivial

### 2)	operations

* search: O(h)
* insert: O(h)
* erase: O(h)
  * leaf node
  * degree 1 node
  * degree 2 node: replace with the element in right sub-tree, then delete the root of right sub-tree

### 3)	Find BST given pre-order

* trivial



## 10.	AVL Tree

### 1)	definition

* a BST
* named after ```Adelson-Velskii and Landis```
* $$ |h(left child) - h(right child)| \leq 1 $$
* defined recursively for every child trees

### 2)	Maintenance

* in order to perform the maintenance, we have to perform height function in $$ O(1) $$ time, so we have to add a member variable ```m_treeHeight``` for every node and update it during inserting and erasing.
* after insertion or deletion, we have to check balance for each node in the path up to the root

#### a.	LL case

* trivial

#### b.	LR case

* trivial

### 3)	height

#### a.	minimal case

* clearly, an AVL tree has a minimal height satisfies:

$$
n = 2^{h+1} - 1
$$

#### b.	maximal case

* In the maximal case, the height of the AVL satisfies:

$$
N(h) = N(h-1) + N(h-2) + 1
$$

* we can relate it to Fibonacci number:

$$
N(h) + 1 = (N(h - 1) + 1) + (N(h - 2) + 1)\\
N(h) = Fibo(h + 2)
$$





## 11.	Disjoint Set

### 1)	operations

#### a.	find

* given the representative element of an object

#### b.	set union

* combine two unions

### 2)	Implementation

#### a.	array

- poor implementation
- using two arrays, one for objects and the other for representative object
- O(1) for find, O(n) for union

#### b.	a general tree

* O(h) for find
* O(h) for union

### 3)	Optimizations

#### a.	find

* redirect the parent of the found object to be the root

#### b.	set union

* always set the parent of the root of the shorter tree as the root of the taller tree.



## 12.	Graph

### 1)	definitions

#### a.	degree

* the number of adjacent vertices
* in/out degree

#### b.	path

* trivial
* simple path: no repetitions

#### c.	tree

* connected and unique path between any two vertices
* N nodes with n-1 edges

#### d.	forest

* any graph with no cycles

#### e.	sources and sinks

* source: in-degree 0
* sink: out-degree 0

### 2)	Properties

#### a.	#edges and #vertices

$$
|E| \leq 2\binom{|V|}{2} = 2 \frac{|V|(|V| - 1)}{2} = |V|(|V| - 1) = O(|V|^2)
$$

### 3)	representations

#### a.	adjacency matrix

* $$ \Theta(n^2) $$ memory complexity
* use $$ n \times n $$ matrix to store edges
* many memory waste, but $$ \Theta(1) $$ for finding path

#### b.	adjacency list

* use an array of linked list to store edges

* save memory, but find path requires:
  $$
  |E| \leq 2\binom{|V|}{2} = 2 \frac{|V|(|V| - 1)}{2} = |V|(|V| - 1) = O(|V|^2)
  $$

### 4)	traverse

#### a.	DFS

* based on stack or recursion algorithm
* require a $$ \Theta(|V|) $$ memory to track vertices visited
* time: $$ \Theta(|V| + |E|) $$

#### b.	BFS

* based on queue
* require a $$ \Theta(|V|) $$ memory to track vertices visited
* time: $$ \Theta(|V| + |E|) $$

#### 5)	Applications

* connected ness
* unweighted path length
* bipartite graphs



## 13.	Topological sort

### 1)	DAG(Directed Acyclic Graph)

* a graph is a DAG if and only if it has a topological sorting
* at least one vertex with in-degree zero
* any subgraph is a DAG

### 2)	Algorithm for finding the topological sort

* choose a source v
* let v be the next vertex in sort
* remove v and all edges connected to it
* repeat until done

### 3)	Analysis

* a topological sort need not to be unique
* Use a queue to store vertices with in degree zero
* Runtime: $$ \Theta(|V| + |E|) $$ using adjacency list and $$ \Theta(|V|^2) $$ using matrix
* memory: $$ \Theta(|V|) $$ for in-degree table



## 14.	Minimum Spanning Tree

### 1)	definitions

* weight of a tree: sum of all the weights on all the edges
* given all the weights are distinct, there is a unique minimum spanning tree

### 2)	Tree generation

#### a.	Prim's algorithm

##### i.	steps

* Choose a arbitrary vertex
* iteratively adding the edge with the minimum weight connecting to the current tree
* stop when we have n vertices

##### ii.	implementations

* a Boolean flag ```visited``` for each vertices
* a ```minimum distance``` to the partially constructed tree for each vertices
* a ```parent``` pointer
* using a priority queue to perform BFS

##### iii.	Complexity

* $$ |Theta(|V|) $$ runtime and memory for initialization

* |V|-1 times iteration
* for each iteration, pop closest element O(ln|V|), update distance O(ln(|V|))
* with adjacent list, total runtime is 

$$
O(|V|ln(|V|) + |E|ln(|V|)) = O(|V|ln(|V|))
$$

#### b.	Kruskal's algorithm

##### i.	steps

* Sort the edges by weight
* add the edge with smallest weight if no cycle are formed
* add iteratively until all the edges are considered(if |V| - 1 edges are added, then There is a minimum spanning tree)

##### ii.	implementation

* array for storing and sorting distances
* disjoint set for determining cycle

###### iii.	Complexity

* initialization and sorting: $$ O(|E|ln(|E|)) $$
* average $$ O(1) $$ for disjoint set operation
* total runtime $$ O(|E| ln(|V|)) $$

### 3)	cut property

Let S be any subset of nodes, let e be the least weight edge with exactly one endpoint in S. Then MST T* contains e.