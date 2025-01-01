## do-while Loop
- General do-while Translation
```c
// do-while version
do {
	Body
} while (Test);

//goto version
loop:
	Body
	if (Test)
		goto loop;
```

## While Loop
- jump-to-middle translation 
	- Initial goto starts loop at test
- Used with -o0 (or -og) // compilier option
```c
// while version
while (Test){
	Body
}

// goto version
	goto test;
loop:
	Body
test:
	if (Test)
		goto loop;
done:
```
 - jump-to-middle makes unnecessary jump
	 - do-while conversion
	 - Initial conditional guards entrance to loop
- Used with -o1
```c
// while version
while (Test){
	Body
}

// do-while version
if (!Test)
	goto done;
do{ 
	Body
} while(Test);
done:

// goto version
if (!Test)
	goto done;
loop:
	Body
	if (Test)
		goto loop;
done:
```

## For Loop 
```c
// for version
for (Init; Test; Update){
	Body
}

// while version
Init;
while (Test){
	Body
	Update;

// do-while version
Init
if (!Test)
	goto done;
do{ 
	Body
	Update;
} while(Test);
done:
}
```
- for -> do-while conversion
	- Initial test can be optmized away