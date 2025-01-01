#cpp #datastructure #stack

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20230726165552/Stack-Data-Structure.png)
## Stack Structure
- Linear data structure
- LIFO (Last-In-First-Out)
- Type of Container adaptors 
- Implementation with sequence containers like vactor, list, deque.

## Types (container)
1. Using Deque
2. Using Vector
3. Using List (Linked-LIst)
4. etc..

## Operation

| Basic Operation | Time | Space |
| --------------- | ---- | ----- |
| Top             | O(1) | O(1)  |
| Push            | O(1) | O(1)  |
| Pop             | O(1) | O(1)  |

App~.

## Stack Struct Implementation

- Template 사용
```cpp
template <typename T, typename Container>
struct Stack {
private:
	Container container;

public:

}
```