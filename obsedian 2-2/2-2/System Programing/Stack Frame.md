
- ref : [컴퓨터 구성의 스택 프레임 - GeeksforGeeks](https://www.geeksforgeeks.org/stack-frame-in-computer-organization/)

| Stack Frame Structure                 | Explanation                                   |
| ------------------------------------- | --------------------------------------------- |
| Previous Frame                        |                                               |
| Arguments 7+                          | Caller Frame                                  |
| Return Addr                           | Caller Frame (Pushed by **call** instruction) |
| <font color="#7f7f7f">old %rbp</font> | Frame Pointer %rbp (Optional)                 |
| Saved Registers + Local Variables     |                                               |
| Argument Build (Optional)             | Stack Pointer %rsp                            |

### Contents
- Return information
- Local storage (if needed)
- Temporary space (if needed)

### Management
- Space allocated when enter procedure
	- "Set-up" code
	- Includes push by **call** instruction
- Deallocated when return
	- "Finish" code
	- Includes pop by **ret** instruction
