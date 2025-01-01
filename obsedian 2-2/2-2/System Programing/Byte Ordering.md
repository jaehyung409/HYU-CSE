#endian #big_endian #little_endian
### Ref :[엔디언이란 무엇인가? 빅 엔디언과 리틀 엔디언 - GeeksforGeeks](https://www.geeksforgeeks.org/little-and-big-endian-mystery/)

## What is Endianness?
- Endianness refers to the order in which bytes are arranged in memory.
- Endianness must be considered in various computing scenarios, particularly when systems with different byte orders need to communicate or share data.
![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5d/32bit-Endianess.svg/880px-32bit-Endianess.svg.png)

### Big Endian
- In Sun, PPC Mac, Internet
- Least significant byte has highest address
### Little Endian
- In x86, ARM processors running Android, iOS, and Windows
- Least significant byte has lowest address
- useful for operations.