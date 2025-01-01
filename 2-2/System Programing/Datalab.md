#### 0. Base
- modify "bits.c"
- make
- ./btest -f bitXor 

#### 1. bitXor
- legal ops : ~ &
- Max ops : 14
- 
```c
int bitXor(int x, int y){
  // Symmetric Difference using De Morgan's Laws
  return ~(~(x & ~y) & ~(y & ~x));
}
```

#### 2. tmin
- legal ops : ! ~ & ^ | + << >>
- Max ops : 4
- 
```c
int tmin(void) {
  // Tmin has all bits set to 0 except the sign bit
  return 1 << 31;
}
```

#### 3. isTmax
- legal ops : ! ~ & ^ | +
- max ops : 10
- 2배하고 1더하면 Umax 나오는 거 -1 이랑 Tmax인데 -1을 쳐내
```c
int isTmax(int x) {
  // The cases where 2 * x equals Umax (all bits 1) are -1 and Tmax
  // Exclude -1 from these case using ~x
  return !(~((x+x)+1) ^ !(~x));
}
```

#### 4. allOddBits
- legal ops : ! ~ & ^ | + << >>
- max ops : 12
- d
```c
int allOddBits(int x) {
  // If all bits are odd, AND operation with 0xAAAAAAAA 
  // 	will leave only the odd bits
  // OR operation between this value and (value >> 1)
  int allOdd = (0xAA << 24) | (0xAA << 16) | (0xAA << 8) | 0xAA;
  return !(~((x & allOdd) | ((x & allOdd) >> 1)));
}
```

#### 5. negate
- legal ops : ! ~ & ^ | + << >>
- max ops : 5
- d
```c
int negate(int x) {
  // In two's complement, negate = invering all bits + 1
  return ~x + 1;
}
```

#### 6. isAsciiDigit
- legal ops : ! ~ & ^ | + << >>
- max ops : 15
- 5,6 번쨰 bit가 1인지 확인하고 +7 을 한 값이 0x40보다 작은지 체크
```c
int isAsciDigit(int x) {
  // Check if the 5th and 6th bits are set to 1 (30 <= x <= 3F)
  // Add 7 to the value and verify if the result less than 0x40
  return !((x >> 4) + (~3 + 1)) & !((x + 6) >> 6) ;
}
```

#### 7. conditional
- legal ops : ! ~ & ^ | + << >>
- max ops : 16
- y, z 를 x에 따라 0 또는 자기 자신이 나오도록 세팅
```c
int conditional(int x, int y, int z) {
  // Set y and z to either 0 or to their own values
  // using AND operation with (0 or 0xFFFFFFFF)
  y = y & (~(!!x) + 1);
  z = z & (~(!x) + 1);
  return y | z;
}
```

#### 8. isLessOrEqual
- legal ops : ! ~ & ^ | + << >>
- max ops : 24
- 1. 부호가 다른 경우 : y 가 음수면 0출력
- 2. 부호가 같은 경우 : y -x 음수면 0 출력 
```c
int isLessOrEqual(int x, int y) {
  // If the signs are different and y is negative, output 0
  // If the signs ate the same and y - x is negative,output 0
  int checkXYSign = x ^ y;
  return 1 + (((checkXYSign & y) | (~checkXYSign & (~x + 1 + y))) >> 31);
}
```

#### 9. logicalNeg
- legal ops : ~ & ^ | + << >>
- max ops : 12
- Tmin = -Tmin, 0 = -0 else -연산시 부호가 바뀜 
```c
int logicalNeg(int x) {
  // Except for Tmin and 0, the sign changes,
  // 	when performing the negate operation.
  return 1 + ((x | (~x + 1)) >> 31);
}
```

#### 10. howManyBits
- legal ops : ! ~ & ^ | + << >>
- max ops : 90
- 양수면 1, 음수면 0이 나오는 최고비트를 구함 (Sign 과 XOR 이용)
- 이진탐색을 사용 (마지막에는 check 가 0이 되므로 1을 수기로 더함)
```c
int howManyBits(int x) {
  // Find the highest bit that results in 
  // 	1 for positive numbers and 0 for negative numbers
  // 	using Sign and XOR operations.
  // Use binary search (manually add 1 at the end since check = 0)
  // Add 1 to this result
  int sign = x >> 31;
  int check = 16;
  int ans = 0;
  ans = ans + ((~(!!((x >> (check + ans)) ^ sign)) + 1) & check);
  check = check >> 1;
  ans = ans + ((~(!!((x >> (check + ans)) ^ sign)) + 1) & check);
  check = check >> 1;
  ans = ans + ((~(!!((x >> (check + ans)) ^ sign)) + 1) & check);
  check = check >> 1;
  ans = ans + ((~(!!((x >> (check + ans)) ^ sign)) + 1) & check);
  check = check >> 1;
  ans = ans + ((~(!!((x >> (check + ans)) ^ sign)) + 1) & check);
  ans = ans + ((~(!!((x >> ans) ^ sign)) + 1) & 1);
  return ans + 1;
}
```
#### 11. floatScale2
- legal ops : Any integer/unsigned operations incl. ||, &&. also if, while
- S(sign), E(exp), F(frac)으로 분리 (IEE754에 의거)
- case 1 : normalized
	- E + 1
- case 2 : denormalized
	- F 값 2배 (F << 1)
- case 3 : special
	- uf return
```c
unsigned floatScale2(unsigned uf) {
  // Separate into S, E, and M (IEEE 754)
  // If E == 0xFF (special case). return uf
  // If E == 0 (denormalized case). M << 1 (since M represents 0.x)
  // Else, E + 1
  unsigned int s = uf >> 31;
  unsigned int exp = (uf >> 23) & 0xFF;
  unsigned int Hex7FFFFF = (0x7F << 16) | (0xFF << 8) | 0xFF;
  unsigned int frac = uf & Hex7FFFFF;
  if (exp == 0xFF)
    return uf;
  else if (exp == 0x0)
	return (s << 31) | (frac << 1);
  else
	return (s << 31) | ((exp + 1) << 23) | frac;
}
```
#### 12. floatFloat2Int
- legal ops : Any integer/unsigned operations incl. ||, &&. also if, while
- S(sign), E(exp), F(frac)으로 분리 (IEE754에 의거)
- Integer의 범위의 절댓값은  $2^{31}$ 보다 작다. 
	- E > 158(127 + 31) : return inf
- E < 127 (denormalized) : return 0
- E < 150(127 + 23(F 표현 비트 수)) : >> 150 - E (소수부 제거)
- E > 150(127 + 23) : << E - 150 (정수부 확장)
```c
int floatFloat2Int(unsigned uf) {
  // Separate into S, E, and M (IEEE 754)
  // The abs(integer) can represent up to 2^31
  // Since the bias is 127, if E > 158, out of range
  // E < 127 (denormalized case) return 0
  // Else, since M has 23 bits, devide cases E vs 150(127 + 23)
  // Before operations, E = E | 0x800000 (since, M = 1.x)
  // E < 150, remove the fractional part ( >> )
  // Else, extend the integer part ( << )
  unsigned int s = uf >> 31;
  unsigned int exp = (uf >> 23) & 0xFF;
  unsigned int Hex7FFFFF = (0x7F << 16) | (0xFF << 8) | 0xFF;
  unsigned int frac = uf & Hex7FFFFF;
  frac = frac | (0x80u << 16);
  if (exp > 158)
    return (0x80u << 24);
  else if (exp < 127)
	return 0;
  else if (exp < 150) {
	unsigned int abs = frac >> (150 + ~exp + 1);
	if (s)
	  return ~abs + 1;
	else
	  return abs;
  }
  else {
	unsigned int abs = frac << (exp + ~150 + 1);
	if (s)
	  return ~abs + 1;
	else
	  return abs;
  }
}
```
#### 13. floatPower2
- legal ops : Any integer/unsigned operations incl. ||, &&. also if, while
- S(sign), E(exp), F(frac)으로 분리 (IEE754에 의거)
- x < -149 : less than denormalized -> return 0
- x < -126 : denormalized, F 값 표현 (1 << (x + 149))
- x > 127 : out of range -> return INF
- else E = x + 127(bias), S = 0 (positive), F = 0(== 1.0)
```c
unsigned floatPower2(int x) {
  // Separate into S, E, and M (IEEE 754)
  // If x < -(126 + 23) : too small to be represented denom, 
  // 	return 0 (M has 23 bits)
  // If x > 127 : out of range, return INF
  // If x < -126 : 1 << (x + 126 + 23) : representation M
  // Otherwise, S : 0 (Positive), E : x + 127(bias), M : 0 (== 1.0)
  if (x < (~149 + 1))
    return 0;
  else if (x > 127)
	return (0x7F << 24) | (0x80 << 16);
  else if (x < (~126 + 1))
	return 1 << (x + 149);
  else
	return (x + 127) << 23;
}
```