#datastructure #array #algorithms

## Traversal
```cpp
void Singly_Linked_List<T>::traversal(){
	if (head == Null) return;
	Node<T>* current = head;
	while (current->next != Null){
		std::cout << current->data << ' ';
		current = current->next;
	}
	std::cout << '\n';
}
void Doubly_Linked_List<T>::traversal() // same Singly_Linked_List
void Doubly_Linkde_List<T>::traversal_reverse(){
	if (tail == Null) return;
	Node<T>* current = tail;
	while (tail->prev != Null){
		std::cout << current->data << ' ';
		current = current->prev;
	}
	std::cout << '\n';
}
void Circular_Linked_List<T>::traversal(){
	if (head == Null) return;
	Node<T>* cur = head;
	while (cur->next != head){
		std::cout << cur->data << ' ';
		cur = cur->next;
	}
	std::cout << '\n';
}
```
## Insertion
```cpp
void Singly_Linked_List<T>::insert_after(const T element, const Node<T>& node){
1	if (node == tail || node == NULL) { 
		add(element)
		return;
	} // null인 경우 (head에 삽입하는 것으로 예외처리)
	Node<T>* new_node;
	new_node->data = element;
6	new_node->next = node->next;
	node->next = new_node;
} // Circular_Linked_List의 경우 if ~ else(1,6 line)를 제거.
void Doubly_Linke_List<T>::insert_after(const T elemnet, const Node<T>& node){
	if (node == tail || node == NULL) {
		tail = new_node;
		return;
	} // null인 경우 (head에 삽입하는 것으로 예외처리리)
	Node<T>* new_node;
	new_node->data = element;
	new_node->prev = node;          // new_node->next = node;
	new_node->next = node->next;    // new_node->prev = node->prev;
	node->next = new_node;          // node->prev = new_node;
} // insert_before의 경우 주석 참조
```
## Deletion
```cpp
void Singly_Linked_List<T>::deletion(const T element){
	if (head == Null) return;
2	while (cur != tail && cur->next->data == element){
		cur = cur->next;
	}
5	if (head == tail) return;
	Node<T>* pos = cur->next;
	cur->next = pos->next;
	delete pos;
} // Circular_Linked_List의 경우 while 문 조건에서, head->next != head 로 변경 및 if문 조건을 head->next == head 로 변경. (2,5 line) 
void Doubly_Linked_List<T>::deletion(const Node<T>& node){
	if (node == head && node == tail) delete node;
	else if (node == head){
		node->next->prev == Null;
		delete node;
	}
	else{
		node->prev->next = node->next;
		if (node != tail) node->next->prev = node->prev;
		delete node;
	}
}
```
## Searching
```cpp
Node<T>* Singly_Linked_List<T>::searching(const T element){
	 if (head == Null) return Null;
	 Node<T>* cur = head;
	 while (true){
		 if (cur->data == element) return cur;
		 cur = cur->next;
6		 if (cur == Null) return Null;
	 }
} // Circular_Linked_List의 경우 if (cur == head) 로 변경 (6 line)

```

## Add(Insertion Last)
```cpp
void Singly_Linked_List<T>::add(const T element){
	Node<T>* new_node;
	new_node->data = element;
	new_node->next = NULL; // circular의 경우, new_node->next = head;
	if (get_size() == 0) {
		head = new_node;
		tail = new_node; // circular의 경우, 이 행 대신 new_node->next = head
		return;
	}
	tail->next = new_node;
	tail = new_node;
}//circular의 경우 tail을 따로 정의하지 않았기에, tail을 새로 정의하거나 loop를 통해 직접 찾는 과정이 필요함 ex
// for(auto current = head; current->next != head; current = current->next) { }
// current->next = new_node;
// new_node->next = head;
void Doubly_Linked_List<T>::add(const T element){
	Node<T>* new_node;
	new_node->data = element;
	new_node->prev = new_node->next = NULL;
	if (get_size() == 0) {
		head = tail = new_node; 
		return;
	}
	new_node->prev = tail;
	tail->next = new_node;
	tail = new_node;
}
```