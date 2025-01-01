## General rule: use the highest-level I/O functions you can
- Many C programmers are able to do all of their work using the standard I/O functions
- But, be sure to understand the functions you use!
- When to use [[C Standard IO Functions]]
	- When working with disk or terminal files
- When to use raw [[System IO]] 
	- Inside signal handlers, because Unix I/O is async-signal-safe
	- In rare cases when you need absolute highest performance
- When to use [[Robust IO Package]]
	- When you are reading and writing network sockets
	- Avoid using standard I/O on sockets
## Aside : Working with Binary Files
- Functions you should never use on binary files
	- Text-orientd I/O such as **fgets, scanf, rio_readlineb**
		- Interpret EOL characters
		- Use functions like **rio_readn** or **rio_readnb** instead
	- String functions
		- **strlen, strcpy, strcat**
		- Interprets byte value 0 (end of string) as special