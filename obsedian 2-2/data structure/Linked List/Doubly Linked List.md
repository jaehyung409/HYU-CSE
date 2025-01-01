#datastructure #linked_list #cpp 

## Structure
- Set of Nodes
- Nods : data + two pointes (next / previous node address)
- both direction

## VS Singly Linked List
- more memory (have two pointers)
- Bi-directional Traversals (such as music player's playlist, Undo Operations)
- Deletion of a given node in O(1) (significantly faster than singly)
- implementing deque
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
	Node* prev;
}

template <typename T>
struct Doubly_Linked_List {
private: 
	Node<T>* head;
	Node<T>* tail
	int size = 0;

public:
	Doubly_Linked_List() : head(NULL), tail(NULL) {}
	Doubly_Linked_List(const Singly_Linked_List<T> & sll) {
		for (auto cur = sll.get_head(); cur != sll.get_tail(); cur = cur->next;){
			add(cur->data);
			size++;
		}
	}
	Doubly_Linked_List(const Array<T, N> &arr) {
		for (const auto& element : arr){
			add(element);
			size++;
		}
	}
	~Doubly_Linked_List() {
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
