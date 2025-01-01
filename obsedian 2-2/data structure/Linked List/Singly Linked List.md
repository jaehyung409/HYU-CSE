#datastructure #linked_list #cpp 

## Structure 
- Set of Nodes.
- Node : data + pointer (next node address)
- one-direction 

## Implementation
- Template class 활용
- size 계산을 줄이기 위하여 size instance 사용
- Node Struct 활용
```cpp
// Singly Linked List implementation
template <typename T>
struct Node {
public:
	T data;
	Node* next;
}

template <typename T>
struct Singly_Linked_List {
private:
	Node<T>* head;
	Node<T>* tail;
	int size = 0;

public:
	Singly_Linked_List() : head(NULL), tail(NULL)  {}
	Singly_Linked_List(const Array<T, N> &arr) {
		for (const auto& element : arr){
			add(element);
			size++;
		}
	}
	~Singly_Linked_List() {
		Node<T>* current = head;
		Node<T>* nextNode;
		while (current != NULL) {
			nextNode = current->next;
			delete current;
			current = nextNode;
		}
	}
	get_head() { return head; }
	get_tail() { return tail; }
	get_size() { return size; }
}

```