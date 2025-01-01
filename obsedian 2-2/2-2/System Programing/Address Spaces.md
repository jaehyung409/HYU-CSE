### Systems Using Physical Addressing
![](https://i.imgur.com/moZJed2.png)
- A process uses the same address space as its physical address
	- Two processes can use the same address
- Used in ***simple*** systems like embedded microcontrollers in devices like cars, elevators, and digital picture frames
### Systems Using [[Virtual Memory|Virtual Addressing]]
![](https://i.imgur.com/Xg92GyV.png)
- A process uses virtual address space with the help of **MMU**s
	- Processes can use the same address in their own address space
- Used in all modern servers, laptops, and smart phones
- One of the great idea in computer science
### Address Spaces
- Linear address space : Ordered set of contiguous nonnegative integer addresses
- Virtual address space : Set of $N=2^n$ virtual addresses
- Physical address space : Set of $M=2^m$ physical addresses