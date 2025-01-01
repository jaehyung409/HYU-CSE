#cpp #datastructure #algorithms #tree #sorting

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20221220165711/MinHeapAndMaxHeap1.png)

## Heap Structure
- Tree-based data structure (nearly complete binary tree)
- Priority : A\[PARENT(i)] $\geq$ A\[i] 
- [Binary Heap is typically represented as an array](https://www.geeksforgeeks.org/array-representation-of-binary-heap/)
	->Root : Arr\[0]
	->Parent (i) : $\lfloor i/2 \rfloor$
	->left child (i) : $2i$
	->right childe (i) : $2i+1$
## Types
1. Max Heap
2. Min Heap
3. etc

## Operation
## [Applications, Advantages and Disadvantages of Heap](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/)
- Applications 
	- priority queue
	- [[Heap Sort]]
	- Graph algorithms
- Advantages
	- Efficient insertion and deletion
	- Guaranteed access to the priority element
	- Space efficiency
- Disadvantages
	- Lack of flexibility
	- Not ideal for searching
	- Not a stalve data structure

## Heap struct Implementation