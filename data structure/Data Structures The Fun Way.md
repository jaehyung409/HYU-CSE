#datastructure

[[Data Structure The Fun Way.excalidraw]]
## Array
- 관련된 다수의 값을 저장할 때 사용한다. 
- Index Based with offset. (메모리의 연속된 부분에 저장)
- Fixed (Non-Dynamic) -> Insertion / Deletion ...
```pseudocode
ArrayDouvle (Array : old_array):
	Integer : length = len(old_array)
	Array : new_array = Array[2 * length] // 크기가 2배인 새로운 배열
	
	Integer : j = 0
	WHILE j < length:
		new_array[j] = old_array[j]
		j = j + 1
	return new_array
```

## Linked List
