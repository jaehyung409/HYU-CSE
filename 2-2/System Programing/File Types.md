## File Types
- Each file has a *type* indicating its role in the system
	- Regular file : Contains aribitary data
	- Directory : Index for a related group of files
	- Socket : For communicating with a process on another machine
- Other file types betyond our scope
	- Named pipes (FIFOs)
	- Symbolic links
	- Character and block devices 

## Regular Files
> A regular file contains arbitrary data

- Applications often distinguish between text files and binary files
	- Text files are regular files with only ASCII or Unicode characters
	- Binary files are everything else
	 	- e.g., object files, JPEG images
	- Kernal does not know the difference!
- Text file is sequence of text lines
	- Text line is sequence of chars terminated by newline char (`'\n'`)
		- Newline is `0xa`, same as ASCII line feed character (LF)
- End of line (EOL) indicators in other systems
	- Linux and Mac OS : `\n (0xa)`
		- line feed (LF)
	- Windows and Internet protocols : `\r \n (0xd 0xa)`
		- Carrage return (CR) followed by line feed (LF)
## Directories
> Directory consists of an array of links
> 	Each link maps a *filename* to a file
- Each directory contains at **least two** entries
	- <font color="#d99694">.</font> (dot) is a link to itself
	- <font color="#d99694">..</font> (dot doat) is a link to the parent directory in the directory hierarchy
- Commands for manipulating directories
	- $\text{mkdir}$ : create empty directory
	- $\text{ls}$ : view directory contents
	- $\text{rmdir}$ : delete empty directory
- ### Directory Hierarchy
	> All files are organized as a hierachy anchored by root directory name <font color="#d99694">/</font> (slash)
	- ![](https://i.imgur.com/sOmU0lb.png)
		- Kernal maintains current working directory (***cwd***) for each process (ref, command $\text{pwd}$) 
			- Modified using the $\text{cd}$ command
		- Pathnames
			- Locations of files in the hierarchy deenoted by *pathnames* (cwd : /home/you)
				- Absolute pathname starts with '/' and denotes path from root <font color="#d99694">/</font>
					- <font color="#d99694">/</font>home/bob/hello.c
				- Relative pathname denotes path from current working directory
					- <font color="#d99694">../</font>home/bob/hello.c