## Short Counts
- Can occur in these situations 
	- Encountering (end-of-file) **EOF** on reads
	- Reading text lines from a **terminal**
	- Reading and writing **network sockets**
- Never occur in these situations (OS control)
	- Reading from disk files (except for EOF)
	- Writing to disk files
- Best practice is to always allow for short counts