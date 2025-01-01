#datastructure #array #algorithms

## Traversal
```cpp
for (const auto& element : array){
	std::cout << element << ' ';
}
```
## Insertion
```cpp
void Array<T, N>::insert(const T element, const int index){
	if (index >= N)
		throw std::out_of_range();
	for (int i = N-2; i >= index; i--){
		data[i+1] = data[i];
	}
	data[inedx] = element;
}
```
## Deletion
```cpp
void Array<T, N>::deletion(const T element){
	const int index = searching(element);
	if (index == -1) return;
	for (int i = index; i < N-1; i++){
		data[i] = data[i+1]
	}
}
```
## Searching
```cpp
int Array<T, N>::searching(const T element){
	for (int i = 0; i < N; i++){
		if (data[i] == element){
			return i;
		}
	}
	return -1 
} // using searching algorithms if ordered array
```
