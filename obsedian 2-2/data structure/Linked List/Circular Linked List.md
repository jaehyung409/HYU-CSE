#datastructure #linked_list #cpp 

## Structure
- Set of Nodes
- Node : data + pointer (next node address)
- no beginning or end (Linked List with tail node's pointer has head node's address)

## VS Singly
- harder to find th end of the list (can make infinite loop)
- any node can be a starting point
- repeatedly go around the list
- circular doubly list implement Fibonacci Heap
## Implementation
- Template class 활용
- size 계산을 줄이기 위하여 size instance 사용
- Node Struct 활용
```cpp
template <typename T>
struct Node {
public:
	T data;
	Node* next;
}

template <typename T>
struct Circular_Linked_List {
private: 
	Node<T>* head;
	int size = 0;

public:
	Circular_Linked_List() : head(NULL) {}
	Circular_Linked_List(const Array<T, N> &arr) {
		for (const auto& element : arr){
			add(element);
			size++;
		}
	}
	~Circular_Linked_List() {
		Node<T>* current = head;
		Node<T>* nextNode;
		while (current != NULL) {
			nextNode = current->next;
			delete current;
			current = nextNode;
		}
	}
	get_head() { return head; }
	get_size() { return size; }
}
```