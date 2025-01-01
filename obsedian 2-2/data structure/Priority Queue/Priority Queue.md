#cpp #datastructure #algorithms #sorting 


![](https://media.geeksforgeeks.org/wp-content/uploads/20240410101419/Getting-Started-with-Array-Data-Structure.webp)
## Priority Queue Structure
- Linear data structure 
- fixed size (fixed memory size)
- same type, contiguous memory allocation
- Index base (quick access) : base address + offset
	-> base address (address of first element)
	-> offset (difference in the position of the first)
	ex) $N th : base\,+\,N\,*\,(size\,of\,data\,type)$

## Types
1. One-dimensional Arrays
2. Multidimensional Arrays

## [[Operation of Priority Queue|Operation]]
알고리즘 165p참조

| Basic Operation | Time | Space |
| --------------- | ---- | ----- |
| Insert          | O()  | O(1)  |
| Maximum         | O()  | O(N)  |
| Extract-Max     | O()  | O(N)  |
| Increase-Key    | O()  | O(1)  |
+) Random Access O(1)
## [Applications, Advantages and Disadvantages of Array](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-array-data-structure/)
- Advantages 
	- Efficient access, Memory efficiency
- Disadvantages 
	- Fixed size, Wasted space, Lack of flexibility, Single data type, Operation Complexity

## Array Struct Implementation

- Template 사용 
- [[C++ type#^762a29|Aggregate Type 사용]]
``` cpp
template <typename T, size_t N>
struct Array {
private:
	T data[N];
	
public:
	T& operator[](const int index){
		return data[index];
	}
	const T& operator[](const int index) const {
		return data[index];
	}
};
```