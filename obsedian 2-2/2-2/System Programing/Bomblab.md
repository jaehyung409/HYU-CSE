#### Basic GDB
- Using GDB
- b (func_name) / (\*address of line)
	- i b , d (num), d
- r (run)
	- ni, si, c
- p (\$register)
- x
- printf "%s\n", $(register)
- reference to [[Assembly]]

#### 0. main
- disas main : Can find main func phase_1 ~ 6
#### 1. phase_1 : For NASA, space is still a high priority.
- disas phase_1 : Can find strings_not_equal function (maybe input strings)
- disas strings_not_equal : 
	- Structure : $rdi (input) Vs. $rsi (answer)
		- string_length,
	- printf "%s\n", $rdi : "Input String"
	- printf "%s\n", $rsi : "For NASA, space is still a high priority."
#### 2. phase_2 : 1 2 4 8 16 32
- disas phase_2 : Can find read_six_numbers function (maybe input six numbers)
- disas read_six_numbers : input six num
- disas phase_2 : 
	- p \*(int\*)($rsp) : first num, != 1 -> bomb
	- loop : 
		- add %eax, %eax (eax \*= 2)
		- cmp %eax,0x4(%rbx) (compare to next input number, != bomb)
		- $N_{t+1} = N_t * 2$
#### 3. phase_3 : (many case) 6 512
- disas phase_3 : 
	- Input size > 2 (cmp $0x1, %eax), first num <= 7
	- switch loop (first num) :
		- 1 : 0x273
		- 2 : 0x2d8
		- 3 : 0xfd
		- 4 : 0x13b
		- 5 : 0x2db
		- 6 : 0x200
		- 7 : 0x13b
#### 4. phase_4 : 60 3
- disas phase_4 :
	- input size == 2 (cmp $0x2, %eax)
	- second num : 2 ~ 4.
- disas func4 (recursive func, make on hand)
#### 5. phase_5 : 5 115
- disas phase_5 : 
	- inpust size > 2, first num < 15
	- loop -> with buit-in array : x/64xb 0x5555555571e0(check)
	- arr\[input(first num)] = k
		- arr\[k] = m ... finally  arr\[?] = 15 then loop end
		- loop must be excuted 15
	- second num = 120 - first num
#### 6. phase_6 : 3 6 2 1 5 4
- disas phae_6 :
	- read_six_number : input size == 6.
		- input numbers are distinct and less than 7($\leq 6$)
- loop with node table : x/10gx 0x555555559210(check)
	- I can't find node 6, so let node6 randomly and disas to find it's position.
		- b \*0x0000555555555936 (check)
		- p \*(int\*)\$rbx (check) : you can get node num
	- pair (input num - node num) and sorting node num (decreasing order)
		- node 1 : 0x97
		- node 2 : 0x18e
		- node 3 : 0x212
		- node 4 : 0x037
		- node 5 : 0x076
		- node 6 : 0x1d9